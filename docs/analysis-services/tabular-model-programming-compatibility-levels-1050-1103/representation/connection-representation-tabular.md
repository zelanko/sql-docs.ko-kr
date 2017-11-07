---
title: "연결 표현 (테이블 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 4b410b16-d36e-4185-bb20-922e66e5e2b7
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2fa62e16d603bb9adfff2410d14d376f358273be
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="connection-representation-tabular"></a>연결 표현(테이블 형식)
  연결 개체는 테이블 형식 모델을 채우는 데이터의 원본을 정의합니다.  
  
## <a name="connection-representation"></a>연결 표현  
 연결 개체의 사양은 OLE DB 공급자의 규칙을 따릅니다.  
  
### <a name="connection-in-amo"></a>AMO의 연결  
 AMO를 사용하여 테이블 형식 모델 데이터베이스를 관리하는 경우 AMO의 <xref:Microsoft.AnalysisServices.DataSource> 개체는 연결 논리 개체에 일 대 일로 일치합니다.  
  
 다음 코드 조각에서는 AMO 데이터 원본 또는 테이블 형식 모델의 Connection 개체를 만드는 방법을 보여 줍니다.  
  
```  
  
//Create an OLEDB connection string  
StringBuilder SqlCnxStr = new StringBuilder();  
SqlCnxStr.Append(String.Format("Data Source={0};" ,SQLServer.Text));  
SqlCnxStr.Append(String.Format("Initial Catalog={0};", SQLDatabase.Text));  
SqlCnxStr.Append(String.Format("Persist Security Info={0};", false));  
SqlCnxStr.Append(String.Format("Integrated Security={0};", "SSPI"));  
SqlCnxStr.Append(String.Format("Provider={0}", "SQLNCLI11"));  
String DatasourceCnxString = SqlCnxStr.ToString();  
  
//Verify connection string and connectivity  
System.Data.OleDb.OleDbConnection OleDbCnx = new System.Data.OleDb.OleDbConnection(DatasourceCnxString);  
try  
{  
    OleDbCnx.Open();  
}  
catch ()  
{  
    throw;  
}  
String newDataSourceName = (string.IsNullOrEmpty(DataSourceName.Text) || string.IsNullOrWhiteSpace(DataSourceName.Text)) ? SQLDatabase.Text : DataSourceName.Text;  
AMO.DataSource newDatasource = newDatabase.DataSources.Add(newDataSourceName, newDataSourceName);  
newDatasource.ConnectionString = DatasourceCnxString.Text;  
if (impersonateServiceAccount.Checked)  
    newDatasource.ImpersonationInfo = new AMO.ImpersonationInfo(AMO.ImpersonationMode.ImpersonateServiceAccount);  
else  
{  
    if (String.IsNullOrEmpty(impersonateAccountUserName.Text))  
    {  
        MessageBox.Show(String.Format("Account User Name cannot be blank when using 'ImpersonateAccount' mode"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Information);  
        return;  
    }  
    newDatasource.ImpersonationInfo = new AMO.ImpersonationInfo(AMO.ImpersonationMode.ImpersonateAccount, impersonateAccountUserName.Text, impersonateAccountPassword.Text);  
}  
newDatasource.Update();  
  
```  
  
## <a name="tabular-amo-2012-sample"></a>Tabular AMO 2012 예제  
 AMO를 사용하여 연결 표현을 만들고 조작하려면 Tabular AMO 2012 예제의 원본 코드를 참조하십시오. 특히 다음 원본 파일을 확인하십시오. 특히 원본 파일 Database.cs에서 확인하십시오. 예제는 Codeplex에서 사용할 수 있습니다. 예제 코드는 여기에서 설명한 논리적 개념에 대한 지원으로만 제공되며 프로덕션 환경에서 사용해서는 안 됩니다.  
  
  

