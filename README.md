# Atata.NUnit

[![Atata Templates](https://img.shields.io/badge/get-Atata_Templates-green.svg?color=4BC21F)](https://marketplace.visualstudio.com/items?itemName=YevgeniyShunevych.AtataTemplates)\
[![Slack](https://img.shields.io/badge/join-Slack-green.svg?colorB=4EB898)](https://join.slack.com/t/atata-framework/shared_invite/zt-5j3lyln7-WD1ZtMDzXBhPm0yXLDBzbA)
[![Atata docs](https://img.shields.io/badge/docs-Atata_Framework-orange.svg)](https://atata.io)
[![X](https://img.shields.io/badge/follow-@AtataFramework-blue.svg)](https://x.com/AtataFramework)

**Atata.NUnit** is a C#/.NET library that integrates [Atata](https://github.com/atata-framework/atata) with NUnit.

*The package targets .NET 8.0 and .NET Framework 4.6.2.*

## Features

Atata.NUnit provides seamless integration between Atata Framework and NUnit testing framework, offering:

- **Test suite base classes**. `AtataTestSuite`, `AtataGlobalFixture`, and `AtataNamespaceFixture` for different testing scopes.
- **NUnit-aware context configuration**. Automatic integration of NUnit test names, suite names, traits, and properties.
- **Enhanced assertion strategies**. NUnit-compatible aggregate assertions and warning reporting.
- **Log integration**. Direct logging output to NUnit test context.
- **Error handling**. Built-in Atata error handling (screenshots, page snapshots, etc.) on test failures and attaching artifacts to test results.
- **Parallel test support**. Full support for NUnit's parallel execution capabilities.

## Installation

Install the package via .NET CLI:

```bash
dotnet add package Atata.NUnit
```

Or using Package Manager:

```powershell
Install-Package Atata.NUnit
```

## Usage

### Global fixture

For global setup across all test suites, create a class that inherits from `AtataGlobalFixture`:

```cs
public sealed class GlobalFixture : AtataGlobalFixture
{
    protected override void ConfigureAtataContextGlobalProperties(AtataContextGlobalProperties globalProperties)
    {
        // Configure global properties for AtataContext
    }

    protected override void ConfigureAtataContextBaseConfiguration(AtataContextBuilder builder)
    {
        // Configure base AtataContext configuration
    }

    protected override void ConfigureGlobalAtataContext(AtataContextBuilder builder)
    {
        // Configure global AtataContext
    }

    protected override void OnBeforeGlobalSetup()
    {
        // Custom logic before global setup
    }

    protected override void OnAfterGlobalSetup()
    {
        // Custom logic after global setup
    }

    protected override void OnBeforeGlobalTeardown()
    {
        // Custom logic before global teardown
    }

    protected override void OnAfterGlobalTeardown()
    {
        // Custom logic after global teardown
    }
}
```

All the methods are virtual and are not required to be overridden.
You can choose to override only those that are relevant to your setup.
Mostly you will only need to override `ConfigureAtataContextBaseConfiguration` and `ConfigureGlobalAtataContext`.

### Test suite class

Create a test class that inherits from `AtataTestSuite`:

```cs
public sealed class SampleTests : AtataTestSuite
{
    [Test]
    public void SampleTest()
    {
        // Test method implementation
    }

    protected override void ConfigureSuiteAtataContext(AtataContextBuilder builder)
    {
        // Optional test suite-specific configuration
    }

    protected override void ConfigureTestAtataContext(AtataContextBuilder builder)
    {
        // Optional test method-specific configuration
    }
}
```

### Namespace fixture

Use `AtataNamespaceFixture` for namespace-scoped setup:

```cs
namespace MyTests.Namespace1; // <- Namespace for which the fixture applies

public seales class NamespaceFixture : AtataNamespaceFixture
{
    protected override void ConfigureNamespaceAtataContext(AtataContextBuilder builder)
    {
        // Namespace-specific configuration
    }
}
```

## Custom configuration

If you need to customize Atata context configuration without using base fixture classes,
you can use extension methods for `AtataContextBuilder`.

```cs
builder
    .UseNUnitTestName() // Use NUnit test method name
    .UseNUnitTestSuiteName() // Use NUnit test fixture name
    .UseNUnitTestSuiteType() // Use NUnit test fixture type
    .UseNUnitTestTraits() // Extract traits from NUnit properties
    .UseNUnitAssertionExceptionFactory() // Uses NUnit.Framework.AssertionException as the Atata assertion exception type
    .UseNUnitAggregateAssertionStrategy() // Uses NUnit's Assert.Multiple() for aggregate assertions
    .UseNUnitWarningReportStrategy() // NUnit-compatible warning reporting
    .UseNUnitAssertionFailureReportStrategy() // NUnit assertion failure handling
    .LogConsumers.AddNUnitTestContext() // Log to NUnit test context
    .EventSubscriptions.AddArtifactsToNUnitTestContext();  // Add artifacts to test context
```

## Examples

Check out example projects:
- [Atata Samples / NUnit / Basic Test Project](https://github.com/atata-framework/atata-samples/tree/main/NUnit.BasicTestProject)
- [Atata Samples / NUnit / Advanced Test Project](https://github.com/atata-framework/atata-samples/tree/main/NUnit.AdvancedTestProject)

## Not supported NUnit features

- Static test suites.

## Community

- Slack: [https://atata-framework.slack.com](https://join.slack.com/t/atata-framework/shared_invite/zt-5j3lyln7-WD1ZtMDzXBhPm0yXLDBzbA)
- X: https://x.com/AtataFramework
- Stack Overflow: https://stackoverflow.com/questions/tagged/atata

## Feedback

Any feedback, issues and feature requests are welcome.

If you faced an issue please report it to [Atata.NUnit Issues](https://github.com/atata-framework/atata-nunit/issues),
[ask a question on Stack Overflow](https://stackoverflow.com/questions/ask?tags=atata+csharp) using [atata](https://stackoverflow.com/questions/tagged/atata) tag
or use another [Atata Contact](https://atata.io/contact/) way.

## Contact author

Contact me if you need a help in test automation using Atata Framework, or if you are looking for a quality test automation implementation for your project.

- LinkedIn: https://www.linkedin.com/in/yevgeniy-shunevych
- Email: yevgeniy.shunevych@gmail.com
- Consulting: https://atata.io/consulting/

## Contributing

Check out [Contributing Guidelines](CONTRIBUTING.md) for details.

## SemVer

Atata Framework follows [Semantic Versioning 2.0](https://semver.org/).
Thus backward compatibility is followed and updates within the same major version
(e.g. from 2.1 to 2.2) should not require code changes.

## License

Atata is an open source software, licensed under the Apache License 2.0.
See [LICENSE](LICENSE) for details.
