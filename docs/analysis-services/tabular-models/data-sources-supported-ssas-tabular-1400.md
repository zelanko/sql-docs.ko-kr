---
title: SQL Server Analysis Services 테이블 형식 1400 모델에서 지 원하는 데이터 원본 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 856e15e7365128bc79d119afe267334fb8470832
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38041661"
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1400-models"></a>1400 테이블 형식 모델 SQL Server Analysis Services에서 지 원하는 데이터 원본

[!INCLUDE[ssas-appliesto-sql2017](../../includes/ssas-appliesto-sql2017.md)]

이 문서에서는 1400 호환성 수준의 테이블 형식 모델 SQL Server Analysis Services (SSAS)를 사용 하 여 사용할 수 있는 데이터 원본 유형의 설명입니다. 

1200 및 낮은 호환성 수준의 SSAS 테이블 형식 모델에 대 한 참조 [SQL Server Analysis Services 테이블 형식 1200 모델에서 지 원하는 데이터 원본](data-sources-supported-ssas-tabular.md)합니다.

Azure Analysis Services에 대 한 참조 [Azure Analysis Services에서 지 원하는 데이터 원본](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)합니다.


## <a name="cloud-data-sources"></a>클라우드 데이터 원본

|Azure 데이터 원본  |메모리 내  |DirectQuery  |
|---------|---------|---------|
|Azure SQL 데이터베이스     |   예      |    예      |
|Azure SQL 데이터 웨어하우스     |   예      |   예       |
|Azure BLOB 저장소     |   예       |    아니요      |
|Azure Table Storage    |   예       |    아니요      |
|Azure Cosmos DB      |  예        |  아니요        |
|Azure Data Lake Store     |   예       |    아니요      |
|Azure HDInsight HDFS     |     예     |   아니요       |
|Azure HDInsight Spark (베타)     |   예       |   아니요       |
||||

**공급자**   
메모리 내 모델과 DirectQuery 모델 Azure 데이터 원본에 연결할 SQL Server에 대 한.NET Framework Data Provider를 사용 합니다.

## <a name="on-premises-data-sources"></a>온-프레미스 데이터 원본

### <a name="supported-by-in-memory-and-directquery-models"></a>메모리 내 모델과 DirectQuery 모델에서 지원

|데이터 원본 | 메모리 내 공급자 | DirectQuery 공급자 |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0, Microsoft OLE DB Provider for SQL Server,.NET Framework Data Provider for SQL Server | .NET Framework Data Provider for SQL Server |
| SQL Server 데이터 웨어하우스 |SQL Server Native Client 11.0, Microsoft OLE DB Provider for SQL Server,.NET Framework Data Provider for SQL Server | .NET Framework Data Provider for SQL Server |
| Oracle |Microsoft OLE DB Provider for Oracle에서 Oracle Data Provider for.NET |.NET 용 oracle Data Provider | |
| Teradata |OLE DB Provider for Teradata.NET 용 Teradata Data Provider |.NET 용 Teradata Data Provider | |
| | | |

> [!NOTE]
> 메모리 내 모델에 대 한 OLE DB 공급자는 대규모 데이터에 대 한 더 나은 성능을 제공할 수 있습니다. 동일한 데이터 원본에 대 한 다양 한 공급자를 선택할 경우 OLE DB 공급자를 먼저 시도 합니다.  

### <a name="supported-by-in-memory-models-only"></a>메모리 내 모델에 지원합니다.

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

## <a name="see-also"></a>참고자료

[테이블 형식 1200 모델 SQL Server Analysis Services에서 지 원하는 데이터 원본](data-sources-supported-ssas-tabular.md)

[Azure Analysis Services에서 지 원하는 데이터 원본](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   
