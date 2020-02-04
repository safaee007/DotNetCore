#SignalR Sample in dot net core

### Model

```
public class ChatMessage
{
    public string Sender { get; set; }
    public string Text{ get; set; }
    public DateTime Date { get; set; }
}

   
ChatHub.cs
public class ChatHub : Hub
{
    public async Task sendMessage(string name, string text)
    {
        var message = new Models.ChatMessage();
        message.Sender = name;
        message.Text = text;
        message.Date = DateTime.UtcNow;

        //send to all
        await Clients.All.SendAsync("reciveMessage", 
            message.Sender, 
            message.Text, 
            message.Date);
    }
}

startUP.cs
services.AddSignalR();


//route
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/chathub");
});
