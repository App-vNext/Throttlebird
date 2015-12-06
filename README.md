```
 ______  __ __  ____    ___   ______  ______  _        ___  ____   ____  ____   ___   
|      T|  T  T|    \  /   \ |      T|      T| T      /  _]|    \ l    j|    \ |   \  
|      ||  l  ||  D  )Y     Y|      ||      || |     /  [_ |  o  ) |  T |  D  )|    \ 
l_j  l_j|  _  ||    / |  O  |l_j  l_jl_j  l_j| l___ Y    _]|     T |  | |    / |  D  Y
  |  |  |  |  ||    \ |     |  |  |    |  |  |     T|   [_ |  O  | |  | |    \ |     |
  |  |  |  |  ||  .  Yl     !  |  |    |  |  |     ||     T|     | j  l |  .  Y|     |
  l__j  l__j__jl__j\_j \___/   l__j    l__j  l_____jl_____jl_____j|____jl__j\_jl_____j

```

# Throttlebird
Throttlebird is a simple http request throttler to help limit the number of client requests within a given period of time.

[![NuGet version](https://badge.fury.io/nu/Throttlebird.svg)](https://badge.fury.io/nu/Throttlebird)  [![Build status](https://ci.appveyor.com/api/projects/status/c2xv4a7fqmfml1qy?svg=true)](https://ci.appveyor.com/project/joelhulen/throttlebird)

# Example
In your WebApiConfig file under the App_Start folder of your ASP.NET MVC project, add the below code block within the Register method:

```
// Implement our custom throttling handler to limit API method calls.
// Specify the throttle store, max number of allowed requests within specified timespan,
// and message displayed in the error response when exceeded.
config.MessageHandlers.Add(new ThrottlingHandler(
    new InMemoryThrottleStore(),
    id => 3,
    TimeSpan.FromSeconds(5),
    "You have exceeded the maximum number of allowed calls. Please wait until after the cooldown period to try again."
));
```

This works across all http requests on your site, limiting the number of requests to 3 every 5 seconds. To adjust, simply modify the *id* parameter to the number of requests, and the timespan to any valid TimeSpan value (FromSeconds, FromMinutes, etc.) to the values that work for you.

# More to Come
This is the the first iteration of this library. Future expansions will allow you to selectively apply throttling on specific controller actions through the use of attributes.
