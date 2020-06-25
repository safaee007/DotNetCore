## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/safaee007/DotNetCore/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

### DotNetCore Articles





# Post To ElasticSearch with Authentication
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

# Insert Bulk To ElasticSearch
step 1 : Elasticsearch.Net in nuget
step 2 :


using Elasticsearch.Net;

```Variables
static string serverURLElastic = Environment.GetEnvironmentVariable("ELASTIC_URL") OR "https://......";
static string usernameElastic = Environment.GetEnvironmentVariable("ELASTIC_USERNAME");
static string passwordElastic = Environment.GetEnvironmentVariable("ELASTIC_PASSWORD");

var ElasticSettings = new ConnectionConfiguration(new Uri(serverURLElastic))
                    .ServerCertificateValidationCallback((o, certificate, chain, errors) => true)
                    .ServerCertificateValidationCallback(CertificateValidations.AllowAll)
                    .RequestTimeout(TimeSpan.FromMinutes(2));
                ElasticSettings.BasicAuthentication(usernameElastic, passwordElastic);

                //add in elastic
                var lowlevelClient = new ElasticLowLevelClient(ElasticSettings);
                var postData = PostData.MultiJson(data);
                var indexResponse = lowlevelClient.Bulk<StringResponse>(index, postData, new BulkRequestParameters { SourceEnabled = false });
                string responseStream = indexResponse.Body;
