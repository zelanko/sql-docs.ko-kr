---
title: 개체 탐색기 노드 속성과 함께 사용자 지정 보고서 사용 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: c7b84355-71ba-402d-85af-23826f18b7da
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5941b15c0aea7319d132e05b902133d3d8b986fa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62823700"
---
# <a name="use-custom-reports-with-object-explorer-node-properties"></a>개체 탐색기 노드 속성과 함께 사용자 지정 보고서 사용
  사용자 지정 보고서가 선택한 개체 탐색기 노드의 보고서 매개 변수를 참조하면 사용자 지정 보고서를 해당 노드의 컨텍스트에서 실행할 수 있습니다. 이렇게 하면 사용자 지정 보고서가 현재 컨텍스트(예: 현재 데이터베이스)나 데이터베이스 또는 서버 개체를 사용할 수 있습니다.  
  
  
## <a name="object-explorer-node-report-parameters"></a>개체 탐색기 노드 보고서 매개 변수  
  
|매개 변수 이름|데이터 형식|  
|--------------------|---------------|  
|`ObjectName`|`String`|  
|`ObjectTypeName`|`String`|  
|`Filtered`|`Boolean`|  
|`ServerName`|`String`|  
|`FontName`|`String`|  
|`DatabaseName`|`String`|  
  
## <a name="object-explorer-node-report-parameters-example"></a>개체 탐색기 노드 보고서 매개 변수 예제  
 예제를 실행하려면 다음 절차를 따릅니다.  
  
 **개체 탐색기에서 노드에 대한 보고서 매개 변수 값을 보려면**  
  
1.  다음 예제 코드를 새 텍스트 파일로 복사하고 .rdl 확장명을 사용하여 파일의 이름을 지정합니다.  
  
2.  사용자 지정 보고서에 대해 데이터베이스 서버에 만든 폴더로 보고서 파일을 복사합니다.  
  
3.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 개체 탐색기의 노드를 마우스 오른쪽 단추로 클릭하고 **보고서**를 가리킨 다음 사용자 지정 보고서를 클릭합니다. **파일 열기** 대화 상자에서 사용자 지정 보고서 폴더를 찾고 보고서 파일을 선택한 다음 **열기**를 클릭합니다.  
  
     개체 탐색기 노드에서 새 사용자 지정 보고서를 처음으로 열면 해당 노드의 바로 가기 메뉴에 있는 **사용자 지정 보고서** 의 가장 최근에 사용한 목록에 이 보고서가 추가됩니다. 표준 보고서를 처음으로 열면 이 보고서도 **사용자 지정 보고서**의 가장 최근에 사용한 목록에 표시됩니다. 사용자 지정 보고서 파일을 삭제하면 다음에 이 항목을 선택할 때 가장 최근에 사용한 목록에서 해당 항목을 삭제하라는 메시지가 표시됩니다.  
  
    1.  최근에 사용한 목록에 표시되는 파일 수를 변경하려면 **도구** 메뉴에서 **옵션**을 클릭하고 **환경** 폴더를 확장한 다음 **일반**을 클릭합니다.  
  
    2.  **최근 사용 목록에 n개 파일 표시**의 개수를 조정합니다.  
  
## <a name="custom-report-code-sample"></a>사용자 지정 보고서 코드 예제  
 다음 코드를 사용하여 만드는 보고서에는 개체 탐색기 노드와 관련된 매개 변수가 사용됩니다.  
  
 `<?xml version="1.0" encoding="utf-8"?>`  
  
 `<Report xmlns="https://schemas.microsoft.com/sqlserver/reporting/2005/01/reportdefinition" xmlns:rd="https://schemas.microsoft.com/SQLServer/reporting/reportdesigner">`  
  
 `<ReportParameters>`  
  
 `<ReportParameter Name="ObjectName">`  
  
 `<DataType>String</DataType>`  
  
 `<Nullable>true</Nullable>`  
  
 `<AllowBlank>true</AllowBlank>`  
  
 `<Prompt>ObjectName</Prompt>`  
  
 `</ReportParameter>`  
  
 `<ReportParameter Name="ObjectTypeName">`  
  
 `<DataType>String</DataType>`  
  
 `<Nullable>true</Nullable>`  
  
 `<AllowBlank>true</AllowBlank>`  
  
 `<Prompt>ObjectTypeName</Prompt>`  
  
 `</ReportParameter>`  
  
 `<ReportParameter Name="Filtered">`  
  
 `<DataType>Boolean</DataType>`  
  
 `<Nullable>true</Nullable>`  
  
 `<AllowBlank>true</AllowBlank>`  
  
 `<Prompt>Filtered</Prompt>`  
  
 `</ReportParameter>`  
  
 `<ReportParameter Name="ServerName">`  
  
 `<DataType>String</DataType>`  
  
 `<Nullable>true</Nullable>`  
  
 `<AllowBlank>true</AllowBlank>`  
  
 `<Prompt>ServerName</Prompt>`  
  
 `</ReportParameter>`  
  
 `<ReportParameter Name="FontName">`  
  
 `<DataType>String</DataType>`  
  
 `<DefaultValue>`  
  
 `<Values>`  
  
 `<Value>Tahoma</Value>`  
  
 `</Values>`  
  
 `</DefaultValue>`  
  
 `<AllowBlank>true</AllowBlank>`  
  
 `<Prompt>FontName</Prompt>`  
  
 `</ReportParameter>`  
  
 `<ReportParameter Name="DatabaseName">`  
  
 `<DataType>String</DataType>`  
  
 `<Nullable>true</Nullable>`  
  
 `<DefaultValue>`  
  
 `<Values>`  
  
 `<Value>master</Value>`  
  
 `</Values>`  
  
 `</DefaultValue>`  
  
 `<AllowBlank>true</AllowBlank>`  
  
 `<Prompt>DatabaseName</Prompt>`  
  
 `</ReportParameter>`  
  
 `</ReportParameters>`  
  
 `<DataSources>`  
  
 `<DataSource Name="AllReportParameters">`  
  
 `<ConnectionProperties>`  
  
 `<IntegratedSecurity>true</IntegratedSecurity>`  
  
 `<ConnectString>Data Source=.</ConnectString>`  
  
 `<DataProvider>SQL</DataProvider>`  
  
 `</ConnectionProperties>`  
  
 `<rd:DataSourceID>f1feee4c-0fdc-4301-9efa-3cd89eed2d9f</rd:DataSourceID>`  
  
 `</DataSource>`  
  
 `</DataSources>`  
  
 `<BottomMargin>1in</BottomMargin>`  
  
 `<RightMargin>1in</RightMargin>`  
  
 `<rd:DrawGrid>true</rd:DrawGrid>`  
  
 `<InteractiveWidth>8.5in</InteractiveWidth>`  
  
 `<rd:SnapToGrid>true</rd:SnapToGrid>`  
  
 `<Body>`  
  
 `<ReportItems>`  
  
 `<Textbox Name="textbox1">`  
  
 `<rd:DefaultName>textbox1</rd:DefaultName>`  
  
 `<ZIndex>1</ZIndex>`  
  
 `<Width>6in</Width>`  
  
 `<Style>`  
  
 `<PaddingLeft>2pt</PaddingLeft>`  
  
 `<PaddingBottom>2pt</PaddingBottom>`  
  
 `<FontFamily>Tahoma</FontFamily>`  
  
 `<FontWeight>700</FontWeight>`  
  
 `<FontSize>20pt</FontSize>`  
  
 `<Color>SteelBlue</Color>`  
  
 `<PaddingRight>2pt</PaddingRight>`  
  
 `<PaddingTop>2pt</PaddingTop>`  
  
 `</Style>`  
  
 `<CanGrow>true</CanGrow>`  
  
 `<Height>0.36in</Height>`  
  
 `<Value>AllReportParameters</Value>`  
  
 `</Textbox>`  
  
 `<Table Name="table1">`  
  
 `<DataSetName>AllReportParameters</DataSetName>`  
  
 `<Top>0.36in</Top>`  
  
 `<Details>`  
  
 `<TableRows>`  
  
 `<TableRow>`  
  
 `<TableCells>`  
  
 `<TableCell>`  
  
 `<ReportItems>`  
  
 `<Textbox Name="ObjectName">`  
  
 `<rd:DefaultName>ObjectName</rd:DefaultName>`  
  
 `<ZIndex>5</ZIndex>`  
  
 `<Style>`  
  
 `<BorderStyle>`  
  
 `<Default>Solid</Default>`  
  
 `</BorderStyle>`  
  
 `<PaddingLeft>2pt</PaddingLeft>`  
  
 `<PaddingBottom>2pt</PaddingBottom>`  
  
 `<FontFamily>Tahoma</FontFamily>`  
  
 `<BorderColor>`  
  
 `<Default>LightGrey</Default>`  
  
 `</BorderColor>`  
  
 `<PaddingRight>2pt</PaddingRight>`  
  
 `<PaddingTop>2pt</PaddingTop>`  
  
 `</Style>`  
  
 `<CanGrow>true</CanGrow>`  
  
 `<Value>=Parameters!ObjectName.Value</Value>`  
  
 `</Textbox>`  
  
 `</ReportItems>`  
  
 `</TableCell>`  
  
 `<TableCell>`  
  
 `<ReportItems>`  
  
 `<Textbox Name="ObjectTypeName">`  
  
 `<rd:DefaultName>ObjectTypeName</rd:DefaultName>`  
  
 `<ZIndex>4</ZIndex>`  
  
 `<Style>`  
  
 `<BorderStyle>`  
  
 `<Default>Solid</Default>`  
  
 `</BorderStyle>`  
  
 `<PaddingLeft>2pt</PaddingLeft>`  
  
 `<PaddingBottom>2pt</PaddingBottom>`  
  
 `<FontFamily>Tahoma</FontFamily>`  
  
 `<BorderColor>`  
  
 `<Default>LightGrey</Default>`  
  
 `</BorderColor>`  
  
 `<PaddingRight>2pt</PaddingRight>`  
  
 `<PaddingTop>2pt</PaddingTop>`  
  
 `</Style>`  
  
 `<CanGrow>true</CanGrow>`  
  
 `<Value>=Parameters!ObjectTypeName.Value</Value>`  
  
 `</Textbox>`  
  
 `</ReportItems>`  
  
 `</TableCell>`  
  
 `<TableCell>`  
  
 `<ReportItems>`  
  
 `<Textbox Name="Filtered">`  
  
 `<rd:DefaultName>Filtered</rd:DefaultName>`  
  
 `<ZIndex>3</ZIndex>`  
  
 `<Style>`  
  
 `<BorderStyle>`  
  
 `<Default>Solid</Default>`  
  
 `</BorderStyle>`  
  
 `<PaddingLeft>2pt</PaddingLeft>`  
  
 `<PaddingBottom>2pt</PaddingBottom>`  
  
 `<FontFamily>Tahoma</FontFamily>`  
  
 `<BorderColor>`  
  
 `<Default>LightGrey</Default>`  
  
 `</BorderColor>`  
  
 `<PaddingRight>2pt</PaddingRight>`  
  
 `<PaddingTop>2pt</PaddingTop>`  
  
 `</Style>`  
  
 `<CanGrow>true</CanGrow>`  
  
 `<Value>=Parameters!Filtered.Value</Value>`  
  
 `</Textbox>`  
  
 `</ReportItems>`  
  
 `</TableCell>`  
  
 `<TableCell>`  
  
 `<ReportItems>`  
  
 `<Textbox Name="ServerName">`  
  
 `<rd:DefaultName>ServerName</rd:DefaultName>`  
  
 `<ZIndex>2</ZIndex>`  
  
 `<Style>`  
  
 `<BorderStyle>`  
  
 `<Default>Solid</Default>`  
  
 `</BorderStyle>`  
  
 `<PaddingLeft>2pt</PaddingLeft>`  
  
 `<PaddingBottom>2pt</PaddingBottom>`  
  
 `<FontFamily>Tahoma</FontFamily>`  
  
 `<BorderColor>`  
  
 `<Default>LightGrey</Default>`  
  
 `</BorderColor>`  
  
 `<PaddingRight>2pt</PaddingRight>`  
  
 `<PaddingTop>2pt</PaddingTop>`  
  
 `</Style>`  
  
 `<CanGrow>true</CanGrow>`  
  
 `<Value>=Parameters!ServerName.Value</Value>`  
  
 `</Textbox>`  
  
 `</ReportItems>`  
  
 `</TableCell>`  
  
 `<TableCell>`  
  
 `<ReportItems>`  
  
 `<Textbox Name="FontName">`  
  
 `<rd:DefaultName>FontName</rd:DefaultName>`  
  
 `<ZIndex>1</ZIndex>`  
  
 `<Style>`  
  
 `<BorderStyle>`  
  
 `<Default>Solid</Default>`  
  
 `</BorderStyle>`  
  
 `<PaddingLeft>2pt</PaddingLeft>`  
  
 `<PaddingBottom>2pt</PaddingBottom>`  
  
 `<FontFamily>Tahoma</FontFamily>`  
  
 `<BorderColor>`  
  
 `<Default>LightGrey</Default>`  
  
 `</BorderColor>`  
  
 `<PaddingRight>2pt</PaddingRight>`  
  
 `<PaddingTop>2pt</PaddingTop>`  
  
 `</Style>`  
  
 `<CanGrow>true</CanGrow>`  
  
 `<Value>=Parameters!FontName.Value</Value>`  
  
 `</Textbox>`  
  
 `</ReportItems>`  
  
 `</TableCell>`  
  
 `<TableCell>`  
  
 `<ReportItems>`  
  
 `<Textbox Name="DatabaseName">`  
  
 `<rd:DefaultName>DatabaseName</rd:DefaultName>`  
  
 `<Style>`  
  
 `<BorderStyle>`  
  
 `<Default>Solid</Default>`  
  
 `</BorderStyle>`  
  
 `<PaddingLeft>2pt</PaddingLeft>`  
  
 `<PaddingBottom>2pt</PaddingBottom>`  
  
 `<FontFamily>Tahoma</FontFamily>`  
  
 `<BorderColor>`  
  
 `<Default>LightGrey</Default>`  
  
 `</BorderColor>`  
  
 `<PaddingRight>2pt</PaddingRight>`  
  
 `<PaddingTop>2pt</PaddingTop>`  
  
 `</Style>`  
  
 `<CanGrow>true</CanGrow>`  
  
 `<Value>=Parameters!DatabaseName.Value</Value>`  
  
 `</Textbox>`  
  
 `</ReportItems>`  
  
 `</TableCell>`  
  
 `</TableCells>`  
  
 `<Height>0.21in</Height>`  
  
 `</TableRow>`  
  
 `</TableRows>`  
  
 `</Details>`  
  
 `<Header>`  
  
 `<TableRows>`  
  
 `<TableRow>`  
  
 `<TableCells>`  
  
 `<TableCell>`  
  
 `<ReportItems>`  
  
 `<Textbox Name="textbox2">`  
  
 `<rd:DefaultName>textbox2</rd:DefaultName>`  
  
 `<ZIndex>11</ZIndex>`  
  
 `<Style>`  
  
 `<BorderStyle>`  
  
 `<Default>Solid</Default>`  
  
 `</BorderStyle>`  
  
 `<PaddingLeft>2pt</PaddingLeft>`  
  
 `<PaddingBottom>2pt</PaddingBottom>`  
  
 `<FontFamily>Tahoma</FontFamily>`  
  
 `<FontWeight>700</FontWeight>`  
  
 `<FontSize>11pt</FontSize>`  
  
 `<BorderColor>`  
  
 `<Default>LightGrey</Default>`  
  
 `</BorderColor>`  
  
 `<BackgroundColor>SteelBlue</BackgroundColor>`  
  
 `<Color>White</Color>`  
  
 `<PaddingRight>2pt</PaddingRight>`  
  
 `<PaddingTop>2pt</PaddingTop>`  
  
 `</Style>`  
  
 `<CanGrow>true</CanGrow>`  
  
 `<Value>ObjectName</Value>`  
  
 `</Textbox>`  
  
 `</ReportItems>`  
  
 `</TableCell>`  
  
 `<TableCell>`  
  
 `<ReportItems>`  
  
 `<Textbox Name="textbox3">`  
  
 `<rd:DefaultName>textbox3</rd:DefaultName>`  
  
 `<ZIndex>10</ZIndex>`  
  
 `<Style>`  
  
 `<BorderStyle>`  
  
 `<Default>Solid</Default>`  
  
 `</BorderStyle>`  
  
 `<PaddingLeft>2pt</PaddingLeft>`  
  
 `<PaddingBottom>2pt</PaddingBottom>`  
  
 `<FontFamily>Tahoma</FontFamily>`  
  
 `<FontWeight>700</FontWeight>`  
  
 `<FontSize>11pt</FontSize>`  
  
 `<BorderColor>`  
  
 `<Default>LightGrey</Default>`  
  
 `</BorderColor>`  
  
 `<BackgroundColor>SteelBlue</BackgroundColor>`  
  
 `<Color>White</Color>`  
  
 `<PaddingRight>2pt</PaddingRight>`  
  
 `<PaddingTop>2pt</PaddingTop>`  
  
 `</Style>`  
  
 `<CanGrow>true</CanGrow>`  
  
 `<Value>ObjectTypeName</Value>`  
  
 `</Textbox>`  
  
 `</ReportItems>`  
  
 `</TableCell>`  
  
 `<TableCell>`  
  
 `<ReportItems>`  
  
 `<Textbox Name="textbox4">`  
  
 `<rd:DefaultName>textbox4</rd:DefaultName>`  
  
 `<ZIndex>9</ZIndex>`  
  
 `<Style>`  
  
 `<BorderStyle>`  
  
 `<Default>Solid</Default>`  
  
 `</BorderStyle>`  
  
 `<PaddingLeft>2pt</PaddingLeft>`  
  
 `<PaddingBottom>2pt</PaddingBottom>`  
  
 `<FontFamily>Tahoma</FontFamily>`  
  
 `<FontWeight>700</FontWeight>`  
  
 `<FontSize>11pt</FontSize>`  
  
 `<BorderColor>`  
  
 `<Default>LightGrey</Default>`  
  
 `</BorderColor>`  
  
 `<BackgroundColor>SteelBlue</BackgroundColor>`  
  
 `<Color>White</Color>`  
  
 `<PaddingRight>2pt</PaddingRight>`  
  
 `<PaddingTop>2pt</PaddingTop>`  
  
 `</Style>`  
  
 `<CanGrow>true</CanGrow>`  
  
 `<Value>Filtered</Value>`  
  
 `</Textbox>`  
  
 `</ReportItems>`  
  
 `</TableCell>`  
  
 `<TableCell>`  
  
 `<ReportItems>`  
  
 `<Textbox Name="textbox5">`  
  
 `<rd:DefaultName>textbox5</rd:DefaultName>`  
  
 `<ZIndex>8</ZIndex>`  
  
 `<Style>`  
  
 `<BorderStyle>`  
  
 `<Default>Solid</Default>`  
  
 `</BorderStyle>`  
  
 `<PaddingLeft>2pt</PaddingLeft>`  
  
 `<PaddingBottom>2pt</PaddingBottom>`  
  
 `<FontFamily>Tahoma</FontFamily>`  
  
 `<FontWeight>700</FontWeight>`  
  
 `<FontSize>11pt</FontSize>`  
  
 `<BorderColor>`  
  
 `<Default>LightGrey</Default>`  
  
 `</BorderColor>`  
  
 `<BackgroundColor>SteelBlue</BackgroundColor>`  
  
 `<Color>White</Color>`  
  
 `<PaddingRight>2pt</PaddingRight>`  
  
 `<PaddingTop>2pt</PaddingTop>`  
  
 `</Style>`  
  
 `<CanGrow>true</CanGrow>`  
  
 `<Value>ServerName</Value>`  
  
 `</Textbox>`  
  
 `</ReportItems>`  
  
 `</TableCell>`  
  
 `<TableCell>`  
  
 `<ReportItems>`  
  
 `<Textbox Name="textbox6">`  
  
 `<rd:DefaultName>textbox6</rd:DefaultName>`  
  
 `<ZIndex>7</ZIndex>`  
  
 `<Style>`  
  
 `<BorderStyle>`  
  
 `<Default>Solid</Default>`  
  
 `</BorderStyle>`  
  
 `<PaddingLeft>2pt</PaddingLeft>`  
  
 `<PaddingBottom>2pt</PaddingBottom>`  
  
 `<FontFamily>Tahoma</FontFamily>`  
  
 `<FontWeight>700</FontWeight>`  
  
 `<FontSize>11pt</FontSize>`  
  
 `<BorderColor>`  
  
 `<Default>LightGrey</Default>`  
  
 `</BorderColor>`  
  
 `<BackgroundColor>SteelBlue</BackgroundColor>`  
  
 `<Color>White</Color>`  
  
 `<PaddingRight>2pt</PaddingRight>`  
  
 `<PaddingTop>2pt</PaddingTop>`  
  
 `</Style>`  
  
 `<CanGrow>true</CanGrow>`  
  
 `<Value>FontName</Value>`  
  
 `</Textbox>`  
  
 `</ReportItems>`  
  
 `</TableCell>`  
  
 `<TableCell>`  
  
 `<ReportItems>`  
  
 `<Textbox Name="textbox7">`  
  
 `<rd:DefaultName>textbox7</rd:DefaultName>`  
  
 `<ZIndex>6</ZIndex>`  
  
 `<Style>`  
  
 `<BorderStyle>`  
  
 `<Default>Solid</Default>`  
  
 `</BorderStyle>`  
  
 `<PaddingLeft>2pt</PaddingLeft>`  
  
 `<PaddingBottom>2pt</PaddingBottom>`  
  
 `<FontFamily>Tahoma</FontFamily>`  
  
 `<FontWeight>700</FontWeight>`  
  
 `<FontSize>11pt</FontSize>`  
  
 `<BorderColor>`  
  
 `<Default>LightGrey</Default>`  
  
 `</BorderColor>`  
  
 `<BackgroundColor>SteelBlue</BackgroundColor>`  
  
 `<Color>White</Color>`  
  
 `<PaddingRight>2pt</PaddingRight>`  
  
 `<PaddingTop>2pt</PaddingTop>`  
  
 `</Style>`  
  
 `<CanGrow>true</CanGrow>`  
  
 `<Value>DatabaseName</Value>`  
  
 `</Textbox>`  
  
 `</ReportItems>`  
  
 `</TableCell>`  
  
 `</TableCells>`  
  
 `<Height>0.22in</Height>`  
  
 `</TableRow>`  
  
 `</TableRows>`  
  
 `<RepeatOnNewPage>true</RepeatOnNewPage>`  
  
 `</Header>`  
  
 `<TableColumns>`  
  
 `<TableColumn>`  
  
 `<Width>3in</Width>`  
  
 `</TableColumn>`  
  
 `<TableColumn>`  
  
 `<Width>1.5in</Width>`  
  
 `</TableColumn>`  
  
 `<TableColumn>`  
  
 `<Width>0.75in</Width>`  
  
 `</TableColumn>`  
  
 `<TableColumn>`  
  
 `<Width>1.125in</Width>`  
  
 `</TableColumn>`  
  
 `<TableColumn>`  
  
 `<Width>2in</Width>`  
  
 `</TableColumn>`  
  
 `<TableColumn>`  
  
 `<Width>1.375in</Width>`  
  
 `</TableColumn>`  
  
 `</TableColumns>`  
  
 `</Table>`  
  
 `</ReportItems>`  
  
 `<Height>0.79in</Height>`  
  
 `</Body>`  
  
 `<rd:ReportID>abb14e58-fd36-495a-89ff-b66f29ef287b</rd:ReportID>`  
  
 `<LeftMargin>1in</LeftMargin>`  
  
 `<DataSets>`  
  
 `<DataSet Name="AllReportParameters">`  
  
 `<Query>`  
  
 `<rd:UseGenericDesigner>true</rd:UseGenericDesigner>`  
  
 `<CommandText>SELECT 1`  
  
 `</CommandText>`  
  
 `<DataSourceName>AllReportParameters</DataSourceName>`  
  
 `</Query>`  
  
 `<Fields>`  
  
 `<Field Name="ObjectName">`  
  
 `<rd:TypeName>System.String</rd:TypeName>`  
  
 `<DataField>ObjectName</DataField>`  
  
 `</Field>`  
  
 `<Field Name="ObjectTypeName">`  
  
 `<rd:TypeName>System.String</rd:TypeName>`  
  
 `<DataField>ObjectTypeName</DataField>`  
  
 `</Field>`  
  
 `<Field Name="Filtered">`  
  
 `<rd:TypeName>System.Boolean</rd:TypeName>`  
  
 `<DataField>Filtered</DataField>`  
  
 `</Field>`  
  
 `<Field Name="ServerName">`  
  
 `<rd:TypeName>System.String</rd:TypeName>`  
  
 `<DataField>ServerName</DataField>`  
  
 `</Field>`  
  
 `<Field Name="FontName">`  
  
 `<rd:TypeName>System.String</rd:TypeName>`  
  
 `<DataField>FontName</DataField>`  
  
 `</Field>`  
  
 `<Field Name="DatabaseName">`  
  
 `<rd:TypeName>System.String</rd:TypeName>`  
  
 `<DataField>DatabaseName</DataField>`  
  
 `</Field>`  
  
 `</Fields>`  
  
 `</DataSet>`  
  
 `</DataSets>`  
  
 `<Width>6.875in</Width>`  
  
 `<InteractiveHeight>11in</InteractiveHeight>`  
  
 `<Language>en-US</Language>`  
  
 `<TopMargin>1in</TopMargin>`  
  
 `</Report>`  
  
## <a name="see-also"></a>참고 항목  
 [Management Studio의 사용자 지정 보고서](custom-reports-in-management-studio.md)   
 [Management Studio에 사용자 지정 보고서 추가](add-a-custom-report-to-management-studio.md)   
 [사용자 지정 보고서 실행 경고 표시](unsuppress-run-custom-report-warnings.md)  
  
  
