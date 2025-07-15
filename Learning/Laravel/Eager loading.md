#Laravel #theory #queries #optimization

Addresses a common issue in database querying known as the "N+1 query problem"

### The N+1 Query Problem
Imagine you have a model `Post` and each post has many `Comments`
If you want to display all posts along with their comments, you might do something like this:
```
$posts = Post::all();
foreach ($posts as $post) {
    foreach ($post->comments as $comment) {
        echo $comment->content;
    }
}
```
First you fetch all posts (1 query) then 10 comments (10 queries) for only one post with it's comments

### Eager Loading approach
You can fetch a post with its comments in a single query using "`with()`" method:
```
$posts = Post::with('comments')->get();
foreach ($posts as $post) {
    foreach ($post->comments as $comment) {
        echo $comment->content;
    }
}
```
This way we only have 2 queries instead of 11. One for all posts and the second one for it's comments