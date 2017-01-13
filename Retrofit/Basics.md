# getting started information and what’s Retrofit about.
 
 **Introduction**

Retrofit turns your HTTP API into a Java interface.
```
public interface GitHubService {
  @GET("users/{user}/repos")
  Call<List<Repo>> listRepos(@Path("user") String user);
}
```

The Retrofit class generates an implementation of the GitHubService interface.
```
Retrofit retrofit = new Retrofit.Builder()
    .baseUrl("https://api.github.com/")
    .build();

GitHubService service = retrofit.create(GitHubService.class);
```
Each Call from the created GitHubService can make a synchronous or asynchronous HTTP request to the remote webserver.
````
Call<List<Repo>> repos = service.listRepos("octocat");
````
Use annotations to describe the HTTP request:

- URL parameter replacement and query parameter support
- Object conversion to request body (e.g., JSON, protocol buffers)
- Multipart request body and file upload

> REQUEST METHOD

Every method must have an HTTP annotation that provides the request method and relative URL. There are five built-in annotations: GET, POST, PUT, DELETE, and HEAD. The relative URL of the resource is specified in the annotation.
````
@GET("users/list")
````
You can also specify query parameters in the URL.
````
@GET("users/list?sort=desc")
````
> URL MANIPULATION

A request URL can be updated dynamically using replacement blocks and parameters on the method. A replacement block is an alphanumeric string surrounded by { and }. A corresponding parameter must be annotated with @Path using the same string.
````
@GET("group/{id}/users")
Call<List<User>> groupList(@Path("id") int groupId);
````
Query parameters can also be added.
````
@GET("group/{id}/users")
Call<List<User>> groupList(@Path("id") int groupId, @Query("sort") String sort);
````
For complex query parameter combinations a Map can be used.
````
@GET("group/{id}/users")
Call<List<User>> groupList(@Path("id") int groupId, @QueryMap Map<String, String> options);
````
>REQUEST BODY

An object can be specified for use as an HTTP request body with the`` @Body`` annotation.
````
@POST("users/new")
Call<User> createUser(@Body User user);
````
The object will also be converted using a converter specified on the Retrofit instance. If no converter is added, only RequestBody can be used.
