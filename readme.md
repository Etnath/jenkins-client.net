jenkins-client.net
====

__Jenkins REST API client for .Net__

Usage
----
```c#
var client = Client.Create("http://your_jenkins_addr", "username", "password");

foreach(var job in client.GetJobs())
{
    Console.WriteLine(job.name);
    Console.WriteLine(job.lastBuild.result);
}
```

```c#
var job = client.GetJob("job_name");

var item = await job.BuildAsync(new Dictionary<string, string>() {
    ["param1"] = "value1"
    ["param2"] = "value2"
});
Console.WriteLine("Build Queued");

/* ��û�� ���尡 jenkins ���� ť���� ���� ����� �Ű��� �� ���� ����Ѵ�. */
await item.WaitForBuildStart();
Console.WriteLine("Build Started");

/* ��û�� ���尡 �Ϸ�, Ȥ�� �����ɶ����� ����Ѵ�. */
await item.WaitForBuildEnd();
Console.WriteLine("Build Finished");
```

Minimum Requirements
----
* C# 6.0
* .Net 4.5
* jenkins 1.519 (Version that jenkins started to include queued build info in build response)