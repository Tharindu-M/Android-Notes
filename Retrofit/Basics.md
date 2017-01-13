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
