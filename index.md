## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/safaee007/DotNetCore/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

### DotNetCore Articles





# Post To ElasticSearch
if you use elastic search in own program
HTTPS Protocol


public static async Task<string> postToElasticsearch(string url, Dictionary<string, dynamic> postData, string user, string pass)
{
	HttpResponseMessage ELResponse;
	string responseString = string.Empty;

	try
	{
		using (var httpClientHandler = new HttpClientHandler())
		{
			httpClientHandler.ServerCertificateCustomValidationCallback = (message, cert, chain, errors) => { return true; };
			using (var httpClient = new HttpClient(httpClientHandler))
			{
				var byteArray = Encoding.ASCII.GetBytes($"{user}:{pass}");
				httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
				httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

				ELResponse = await httpClient.PostAsync(url, new Managers.UtilitiesManager.JsonContent(postData));
				responseString = await ELResponse.Content.ReadAsStringAsync();
			}
		}
	}
	catch (Exception ex)
	{
		Console.WriteLine("elastic con: " + ex.ToString());
	}

	return responseString;
}

