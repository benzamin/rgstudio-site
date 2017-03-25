+++
title = "Synchronus Code Execution in iOS"
date = "2016-12-26T16:49:03+06:00"
tags = ["ios", "programming"]
categories = ["ios"]
banner = "img/blog/synchronous-code-ios.jpg"
+++


"Asynchronus programming" is a polular term now-a-days. People are talking all over the internet about it. Specially when we have network/API calls, we should keep free the main thread, and do the network calling stuff in the background. Cause if we block the main thread, it won't be able to respond to user interaction such as touch. Async calls can be executed on new/seperate threads synchronously, or can be scheduled in the main/other thread's runloop. For an example, if you want to polulate a tableview/collectionView with some data from server, you need to show a loader, call the API asynchronously, when it finished after some time, show the data and refresh the table/collection view.
<br><br>(Jump: Browse to the [sample code][githubref] on Github)

### Let there be Sync!
But you sometimes need to execute a code block in a "Synchronous" way. That means you want to wait until a line of code or a bunch of code is finished, then let execute the next line. Just like one by one execution, the action will execute in synchronous within the runloop of your app.

### Why & when we need this?

Well, if you want to execute some operations, which depends on each other, you need to run them synchronously. Suppose you have 2 service/API calls, once all of them are finished, you will combine them to show in the view. In this case, you need to know when all of them are loaded, as they might take variable time to load. So you need to keep track when all of them are finished. What we can do? Use a counter may be? Which will be decremented by one after every task is finished, and check when the counter hits zero, then execute the final rendering in the view. But its aot a good idea, using a counter, there are good things already in the iOS sdk to do this.


### Ways of synchronous code execution 
There are several options, like GCD dispatch sync.

```objectivec
dispatch_sync(my_custom_bacground_queue, ^{ /* do your stuff */ });
```

If you want to wait in a line/bunch of code from main queue/thread, and then execute the next line when the previous line/bunch of code is done executing in the background thread, you can use semaphores...

```objectivec
-(id)syncRequest:(id)params
{
	__block NSData *responseData = nil;   
		dispatch_semaphore_t semaphore = dispatch_semaphore_create(0);
        //following API call is inititated from main queue
		[SomeNetworkClass callAPIWithParams:params completionHandler:^(NSData *response, NSError *error) 
		{
        //response callback block is called from background thread
			responseData = [NSData dataWithData:response];
			dispatch_semaphore_signal(semaphore);
		}];
	dispatch_semaphore_wait(semaphore, DISPATCH_TIME_FOREVER); 
	return responseData;
}
```

**NOTE:** If the callback block of the API call is delivered in main thread instead of background thread, you'r app will be stuck in the "dispatch_semaphore_wait" line, cause the main thread will never execute the callback as it is paused and waiting for "dispatch_semaphore_signal" to resume. If you end up in this deadlock situation, make sure that the response callback is executed in the background thread. i.e: For **AFNetworking**, by default all the success/failure callbacks are delivered in the main queue, you have to set the "completionQueue" property of the AFHTTPSessionManager or AFURLSessionManager to a custom queue.


I personally like dispatch groups. Here is a [sample code][githubref] for a class which I use for using dispatch groups. I usually use this class as a singletone so that I can use this from anywhere of my code anytime I want.

<script src="https://gist.github.com/benzamin/d64cc7f7487a518556dc7e65dc3d24e0.js"></script>

You can just copy the class (DispatchGroup.h + DispatchGroup.m) in your project, and use them as shown in the sample MySampleViewController.m, hasle free. 

**Dont forget to explore and star my [github][hughubaccount] repos, comment if you have something in your mind 😊** 

[githubref]: https://gist.github.com/benzamin/d64cc7f7487a518556dc7e65dc3d24e0
[hughubaccount]: https://github.com/benzamin/

