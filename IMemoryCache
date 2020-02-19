# cache in dotnet core
```
private static string CacheKey = "MyCache";
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddControllers();
            services.AddMemoryCache();
        }

        public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
        {
            app.Run(async context =>
            {
                var cache = context.RequestServices.GetService<IMemoryCache>();
                var greeting = cache.Get(CacheKey) as string;

                if (string.IsNullOrEmpty(greeting))
                {
                    var options = new MemoryCacheEntryOptions().SetAbsoluteExpiration(TimeSpan.FromMinutes(100));

                    var message = "Hello " + DateTimeOffset.UtcNow.ToString();
                    cache.Set(CacheKey, message, options);
                    greeting = message;
                }
                if (CacheKey == "MyCache")
                {
                    await context.Response.WriteAsync($"Greeting '{greeting}' is cached.");
                } else
                {
                    await context.Response.WriteAsync("Hello World!");
                }
            });

            app.UseRouting();
            app.UseEndpoints(endpoints =>
            {
                endpoints.MapControllers();
                //endpoints.MapGet("/", async context =>
                //{
                //    await context.Response.WriteAsync("Hello World!");
                //});
            });
        }
