---
title: SQL Server Analysis Services 테이블 형식 1400 모델에서 지원 되는 데이터 원본 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1b511ac6d9cf4d75faddf569fcc2391317f19629
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/08/2018
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1400-models"></a>테이블 형식 1400 모델 SQL Server Analysis Services에서 데이터 원본 지원

[!INCLUDE[ssas-appliesto-sql2017](../../includes/ssas-appliesto-sql2017.md)]

이 문서에는 SQL Server Analysis Services (SSAS) 1400 호환성 수준에서 테이블 형식 모델과 함께 사용할 수 있는 데이터 원본의 형식을 설명 합니다. 

SSAS 및 하 한 1200 호환성 수준의 테이블 형식 모델을 참조 하십시오. [SQL Server Analysis Services 테이블 형식 1200 모델에서 지원 되는 데이터 원본](data-sources-supported-ssas-tabular.md)합니다.

Azure Analysis Services에 대 한 참조 [Azure Analysis Services에서 지원 되는 데이터 원본](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)합니다.


## <a name="cloud-data-sources"></a>클라우드 데이터 원본

|Azure 데이터 원본  |메모리 내  |DirectQuery  |
|---------|---------|---------|
|Azure SQL Database     |   예      |    예      |
|Azure SQL 데이터 웨어하우스     |   예      |   예       |
|Azure BLOB 저장소     |   예       |    아니요      |
|Azure 테이블 저장소    |   예       |    아니요      |
|Azure Cosmos DB      |  예        |  아니요        |
|Azure 데이터 레이크 저장소     |   예       |    아니요      |
|Azure HDInsight HDFS     |     예     |   아니요       |
|Azure HDInsight Spark (베타)     |   예       |   아니요       |
||||

**공급자**   
메모리 내 모드와 Azure 데이터 원본에 연결 하는 DirectQuery 모델 SQL Server에 대 한.NET Framework Data Provider를 사용 합니다.

## <a name="on-premises-data-sources"></a>온-프레미스 데이터 원본

### <a name="supported-by-in-memory-and-directquery-models"></a>메모리 내 모델과 DirectQuery 모델에서 지원

|데이터 원본 | 메모리 내 공급자 | DirectQuery 공급자 |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0 Microsoft OLE DB Provider for SQL Server,.NET Framework Data Provider for SQL Server | .NET Framework Data Provider for SQL Server |
| SQL Server 데이터 웨어하우스 |SQL Server Native Client 11.0 Microsoft OLE DB Provider for SQL Server,.NET Framework Data Provider for SQL Server | .NET Framework Data Provider for SQL Server |
| Oracle |Microsoft OLE DB Provider for Oracle Oracle Data Provider for.NET |Oracle Data Provider for.NET | |
| Teradata |OLE DB Provider for Teradata.NET에 대 한 Teradata 데이터 공급자 |.NET에 대 한 Teradata 데이터 공급자 | |
| | | |

> [!NOTE]
> 메모리 내 모델에 대 한 OLE DB 공급자는 대규모 데이터에 대 한 더 나은 성능을 제공할 수 있습니다. 동일한 데이터 원본에 대 한 다른 공급자 중에서 선택 하는 경우 OLE DB 공급자를 먼저 시도 합니다.  

### <a name="supported-by-in-memory-models-only"></a>메모리 내 모델에만 해당 지원

|데이터베이스  |
|---------|---------|---------|
|Access 데이터베이스     | 
|SQL Server Analysis Services     | 
|IBM Informix (베타) | 
|JSON 문서     | 
|이진 파일에서 줄     | 
|MySQL 데이터베이스     | 
|PostgreSQL 데이터베이스    | 예 | 아니요
|SAP HANA   | 예 | 아니요
|SAP Business Warehouse    | 예 | 아니요
|Sybase 데이터베이스     | 예 | 아니요
|||

|파일  |  
|---------|---------|
|Excel 통합 문서     |
|Folder     | 
|JSON | 
|Text/CSV    | 
|XML 테이블    | 
|||

|온라인 서비스  |  
|---------|---------|
|Dynamics 365      |
|Exhange 온라인     |
|Saleforce 개체    | 
|Salesforce 보고서     |
|SharePoint Online 목록     |
|||

|기타  |  
|---------|---------|
|Active Directory      | 
|Exhange     |  
|OData 피드     | 
|ODBC 쿼리     | 
|OLE DB  | 
|SharePoint 목록 | 
|||

## <a name="see-also"></a>참고 항목

[테이블 형식 1200 모델 SQL Server Analysis Services에서 데이터 원본 지원](data-sources-supported-ssas-tabular.md)

[Azure Analysis Services에서 지원 되는 데이터 원본](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   
