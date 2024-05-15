# 📚 AntiBypass API Documentation

Welcome to the AntiBypass API documentation! This guide will help you understand how to use our library to keep your applications secure. Let's get started! 🚀

## Overview

AntiBypass is a C# .NET library designed to protect your applications from threats. It includes methods to:

- 🔍 Check assemblies for hooks.
- 🚫 Detect sniffers.
- 🔒 Secure connections for downloading files, strings, etc.

## Methods

### 🔍 CheckHooks

This method checks an assembly for hooks (nasty stuff that can bypass or crack your app).

#### Syntax

```csharp
public Task<bool> CheckHooks(Assembly assembly, Tuple<bool, string> canLog = null, bool compat = false)
```

#### Parameters

- **assembly** (Assembly): The assembly to check.
- **canLog** (Tuple<bool, string>, optional): Logging options. Default is `null`.
- **compat** (bool, optional): Compatibility flag. Default is `false`.

#### Returns

- **Task<bool>**: A task that returns `true` if hooks are found, `false` otherwise.

#### Example

```csharp
Assembly myAssembly = Assembly.GetExecutingAssembly();
var result = await AntiBypass.CheckHooks(myAssembly, new Tuple<bool, string>(true, "Discord Webhook"), true);

if(result)
{
    Console.WriteLine("🛑 Hooks detected!");
}
else
{
    Console.WriteLine("✅ No hooks detected.");
}
```

### 🚫 CheckSniffer

This method checks for sniffers (tools that spy on your app like HTTPDebugger, Fiddler, Charles).

#### Syntax

```csharp
public bool CheckSniffer()
```

#### Returns

- **bool**: `true` if a sniffer is detected, `false` otherwise.

#### Example

```csharp
bool isSnifferDetected = AntiBypass.CheckSniffer();

if(isSnifferDetected)
{
    Console.WriteLine("🛑 Sniffer detected!");
}
else
{
    Console.WriteLine("✅ No sniffer detected.");
}
```

### 🔒 SecureConnection

This method secures a connection using SSL certificates (to keep your data safe and private).

#### Syntax

```csharp
public bool SecureConnection(Func<Task> code, List<string> certificates)
```

#### Parameters

- **code** (Func<Task>): The code you want to run securely.
- **certificates** (List<string>): A list of SSL certificates.

#### Returns

- **bool**: `true` if the connection is secured, `false` otherwise.

#### Example

```csharp
List<string> certificates = new List<string> { "cert1", "cert2" };
Func<Task> secureCode = async () =>
{
    // Your download code here
};

bool isConnectionSecured = AntiBypass.SecureConnection(secureCode, certificates);

if(isConnectionSecured)
{
    Console.WriteLine("✅ Connection secured.");
}
else
{
    Console.WriteLine("🛑 Failed to secure connection.");
}
```

## Conclusion

AntiBypass helps you keep your apps safe and secure. Use these methods to check for hooks, detect sniffers, and secure your connections. Stay safe! 🛡️
