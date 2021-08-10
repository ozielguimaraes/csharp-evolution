# C# Evolution
## C# 6

**Exception filters**
```
static void Main()
{
    Console.WriteLine(MakeRequest().Result);
}

public static async Task<string> MakeRequest()
{
    var client = new HttpClient();
    var streamTask = client.GetStringAsync("https://localHost:10000");
    try
    {
        var responseText = await streamTask;
        return responseText;
    }
    catch (HttpRequestException e) when (e.Message.Contains("301"))
    {
        return "Site Moved";
    }
    catch (HttpRequestException e) when (e.Message.Contains("404"))
    {
        return "Page Not Found";
    }
    catch (HttpRequestException e)
    {
        return e.Message;
    }
}
```
**Before exception filter**
```
static void Main()
{
    Console.WriteLine(MakeRequest().Result);
}

public static async Task<string> MakeRequest()
{
    var client = new HttpClient();
    var streamTask = client.GetStringAsync("https://localHost:10000");
    try
    {
        var responseText = await streamTask;
        return responseText;
    }
    catch (HttpRequestException e)
    {
        if (e.Message.Contains("301"))
            return "Site Moved";
        else if (e.Message.Contains("404"))
            return "Page Not Found";
        else return e.Message;
    }
}
```
✨  Reference -> https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/when

## Development

**Want to contribute? Great!**
Just submit a PR 🙂


## License

MIT

**Free Software, Hell Yeah!**
