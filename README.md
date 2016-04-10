#### DoddleReport generates tabular reports from any IEnumerable datasource.

Out of the box it can render reports to Excel, PDF, HTML, and CSV – fully pluggable of course. I designed the project to provide reporting output over the LINQ queries we had already written for the application, but maybe you can find other uses for it.

### New to DoddleReport?

*   Look at the [[Building your first report]] page
*   If you’re using ASP.NET make sure to check out [[ASP.NET Reporting]] section
*   Review the ```DoddleReport.Sample.Web``` project in the solution
*   Check out the [[Wiki]] for advanced customization and configuration

### Find it on NuGet

DoddleReport has been split into multiple packages to support more users’ needs. See their Descriptions within NuGet for more on the differences

*   **Install-Package DoddleReport**
*   **Install-Package DoddleReport.Web**
*   **Install-Package DoddleReport.iTextSharp**
*   **Install-Package DoddleReport.AbcPdf**
*   **Install-Package DoddleReport.OpenXml**

### So what does it generate?

The following samples are generated live in real-time (notice the data will change every time you open the report)

### Excel Report (OpenXML)

*   Creates a native Excel file using OpenXML
*   Requires the DoddleReport.OpenXml package
*   Automatic Sticky/Frozen Headers stay at the top when scrolling through the data
*   [**See it live!**](http://doddlereport.azurewebsites.net/Doddle/ProductReport.xlsx)

[![doddlexlsreport](http://download.codeplex.com/download?ProjectName=doddlereport&DownloadId=204393 "doddlexlsreport")](http://download.codeplex.com/download?ProjectName=doddlereport&DownloadId=204392)


### PDF Report (using iTextSharper)

*   Automatically repeats title and column headers numbers on every page
*   Requires the DoddleReport.iTextSharp package
*   [**See it live!**](http://doddlereport.azurewebsites.net/Doddle/productreport.pdf)


### PDF Report (ABCpdf)

*   Automatically repeats title, column headers, and page numbers on every page
*   Requires the DoddleReport.AbcPdf package
*   _Requires an_ [_ABCpdf license_](http://www.websupergoo.com/products.htm#pd)
*   [**See it live!**](http://doddlereport.azurewebsites.net/AbcPdf/ProductReport.pdf)


[![image](http://download.codeplex.com/Download?ProjectName=doddlereport&DownloadId=310428 "image")](http://download.codeplex.com/Download?ProjectName=doddlereport&DownloadId=310427)


### CSV/Delimited

*   Use any kind of delimiter you want
*   [**See it live!**](http://doddlereport.azurewebsites.net/Doddle/productreport.txt)

[![doddleTxtReport](http://download.codeplex.com/download?ProjectName=doddlereport&DownloadId=204395 "doddleTxtReport")](http://download.codeplex.com/download?ProjectName=doddlereport&DownloadId=204394)


### HTML Report

*   Good old HTML report
*   [**See it live!**](http://doddlereport.azurewebsites.net/Doddle/productreport.html)


 [![doddleHtmlReport](http://download.codeplex.com/download?ProjectName=doddlereport&DownloadId=204399 "doddleHtmlReport")](http://download.codeplex.com/download?ProjectName=doddlereport&DownloadId=204398) |

### Basic Usage

```csharp
// Get the data for the report (any IEnumerable will work) 
var query = ProductRepository.GetAll();

var totalProducts = query.Count;
var totalOrders = query.Sum(p => p.OrderCount);

// Create the report and turn our query into a ReportSource 
var report = new Report(query.ToReportSource());

// Customize the Text Fields report.TextFields.Title = "Products Report";
report.TextFields.SubTitle = "This is a sample report showing how Doddle Report works";
report.TextFields.Footer = "Copyright 2011 © The Doddle Project";
report.TextFields.Header = string.Format(@"
    Report Generated: {0}
    Total Products: {1}
    Total Orders: {2}
    Total Sales: {3:c}", DateTime.Now, totalProducts, totalOrders, totalProducts * totalOrders);

// Render hints allow you to pass additional hints to the reports as they are being rendered 
report.RenderHints.BooleanCheckboxes = true;

// Customize the data fields report.DataFields["Id"].Hidden = true;
report.DataFields["Price"].DataFormatString = "{0:c}";
report.DataFields["LastPurchase"].DataFormatString = "{0:d}";
```
