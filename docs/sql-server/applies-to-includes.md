---
title: SQL Server Applies | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: sqlcmd
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
caps.latest.revision: 155
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d9246a20a51a729bcc9427ccde239e30087b59a8
ms.sourcegitcommit: 90a9a051fe625d7374e76cf6be5b031004336f5a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39228662"
---
# <a name="sql-applies-to-and-includes"></a>SQL ‘적용 대상’ 및 ‘Include’
이 문서의 참조는 Markdown에서 ‘Include’를 사용하여 개별 문서의 실제 텍스트를 변경하지 않고도 쉽게 수정할 수 있습니다. SQL 콘텐츠에는 세 가지 유형(SQL 버전, 적용 대상, 참조 텍스트)의 Include가 있습니다. SQL 버전은 설명하고 있는 SQL 버전(예: SQL 2016과 2017)을 나타내는 데 사용되며, 적용 대상은 문서가 적용되는 SQL Server의 버전(Linux의 SQL Server와 Azure SQL Database)을 나타냅니다. 참조 텍스트는 다른 두 범주에 속하지 않는 Include입니다(예: 고객이 SQL에 대한 도움말을 보기 위해 사용할 수 있는 링크 목록인 도움말 보기 Include). 

이 문서에서는 처음 두 가지 유형의 Include에 대한 참조 지점으로만 사용됩니다. 

## <a name="sql-server-version-includes"></a>SQL Server 버전 Include

SQL 콘텐츠 작성자는 제품 이름과 SQL Server의 버전을 자주 포함해야 합니다. 이처럼, 이름이 변경되는 경우 모든 단일 문서에서 값을 수동으로 업데이트하는 대신 Include가 업데이트됩니다. 이러한 Include는 제품 이름의 자리 표시자로 사용되지만 모든 SQL 문서에서 일관되게 사용되지는 않습니다. SQL Server vNext는 아직 버전 번호가 없는 SQL의 향후 릴리스를 가리키며, 위 내용에 대해 예외입니다.  

|SQL 버전| 파일 이름| Markdown 예제 |텍스트 모드|
| :------------  | :-------------| :----------| :-------------------|
|   SQL 2012    |   sssql11-md.md   |   `[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]`    |   SQL Server 2012(11.x)  |
|   SQL 2012 SP1    |   sssql11sp1-md.md    |   `[!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]`  |   SQL Server 2012 SP1(11.0.3x)   |
|   SQL 2014    |   sssql14-md.md   |   `[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]`    |   SQL Server 2014(12.x)  |
|   SQL 2016    |   sssql15-md.md   |   `[!INCLUDE[sssql15-md](../includes/sssql15-md.md)]` |   SQL Server 2016(13.x)  |
|   SQL 2017    |   sssql17-md.md   |   `[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]` |   SQL Server 2017(14.x)  |
|   SQL 2017    |   sssqlv14-md.md  |   `[!INCLUDE[sssqlv14](../includes/sssqlv14-md.md)]`  |   SQL Server 2017(14.x)  |
|   SQL vNext   |   sssqlv15-md.md  |   `[!INCLUDE[sssqlv15-md](../includes/sssqlv14-md.md)]` ? |   SQL Server vNext    |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; |  




## <a name="sql-server-non-version-specific-applies-to"></a>SQL Server 비버전별 적용 대상

| 파일 이름| Markdown 예제 |image|
| :-------------| :----------| :-------------------|
| appliesto-ss-asdb-asdw-xxx-md.md  |   `[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]`    | [!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]    |
|   appliesto-ss-asdb-asdw-pdw-md.md    |   `[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]`    | [!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]    |
|   appliesto-ss-asdb-xxxx-pdw-md.md    |   `[!INCLUDE[appliesto-ss-asdb-xxxx-pdw-md.md](../includes/appliesto-ss-asdb-xxxx-pdw-md.md)]`    | [!INCLUDE[appliesto-ss-asdb-xxxx-pdw-md.md](../includes/appliesto-ss-asdb-xxxx-pdw-md.md)]    |
|   appliesto-ss-asdb-xxxx-xxx-md.md    |   `[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]`    | [!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]    |
|   appliesto-ss-asdbmi-xxxx-xxx-md.md  |   `[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md.md](../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]`    | [!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md.md](../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]    |
|   appliesto-ss-xxxx-asdw-pdw-md.md    |   `[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md.md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]`    | [!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md.md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]    |
|   appliesto-ss-xxxx-xxxx-pdw-md.md    |   `[!INCLUDE[appliesto-ss-xxxx-xxxx-pdw-md.md](../includes/appliesto-ss-xxxx-xxxx-pdw-md.md)]`    | [!INCLUDE[appliesto-ss-xxxx-xxxx-pdw-md.md](../includes/appliesto-ss-xxxx-xxxx-pdw-md.md)]    |
|   appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md  |   `[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]`    | [!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]    |
|   appliesto-ss-xxxx-xxxx-xxx-md-winonly.md    |   `[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly.md](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]`    | [!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly.md](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]    |
|   appliesto-ss-xxxx-xxxx-xxx-md.md    |   `[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md.md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]`    | [!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md.md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]    |
|   appliesto-xx-asdb-asdw-xxx-md.md    |   `[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../includes/appliesto-xx-asdb-asdw-xxx-md.md)]`    | [!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../includes/appliesto-xx-asdb-asdw-xxx-md.md)]    |
|   appliesto-xx-asdb-xxxx-xxx-md.md    |   `[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md.md](../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]`    | [!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md.md](../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]    |
|   appliesto-xx-xxxx-asdw-pdw-md.md    |   `[!INCLUDE[appliesto-xx-xxxx-asdw-pdw-md.md](../includes/appliesto-xx-xxxx-asdw-pdw-md.md)]`    | [!INCLUDE[appliesto-xx-xxxx-asdw-pdw-md.md](../includes/appliesto-xx-xxxx-asdw-pdw-md.md)]    |
|   appliesto-xx-xxxx-asdw-xxx-md.md    |   `[!INCLUDE[appliesto-xx-xxxx-asdw-xxx-md.md](../includes/appliesto-xx-xxxx-asdw-xxx-md.md)]`    | [!INCLUDE[appliesto-xx-xxxx-asdw-xxx-md.md](../includes/appliesto-xx-xxxx-asdw-xxx-md.md)]    |
|&nbsp; | &nbsp; | &nbsp; |  
 
## <a name="sql-server-version-specific-applies-to"></a>SQL Server 버전별 적용 대상
이 적용 대상은 문서가 적용되는 SQL 버전을 지정합니다. 

 파일 이름| Markdown 예제 |image|
| :-------------| :----------| :-------------------|
|   tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md  |   `[!INCLUDE[tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md)]`    | [!INCLUDE[tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md)]    |
|   tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md  |   `[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]`    | [!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]    |
|   tsql-appliesto-ss2008-all-md.md |   `[!INCLUDE[tsql-appliesto-ss2008-all-md.md](../includes/tsql-appliesto-ss2008-all-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2008-all-md.md](../includes/tsql-appliesto-ss2008-all-md.md)]  |
|   tsql-appliesto-ss2008-asdb-asdw-pdw-md.md   |   `[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md.md](../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md.md](../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]  |
|   tsql-appliesto-ss2008-asdb-asdw-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md.md](../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md.md](../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]  |
|   tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md |   `[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]  |
|   tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md   |   `[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md](../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md](../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]  |
|   tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]  |
|   tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md   |   `[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md](../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md](../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]  |
|   tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md](../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md](../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]  |
|   tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md   |   `[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]  |
|   tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]  |
|   tsql-appliesto-ss2012-all-md.md |   `[!INCLUDE[tsql-appliesto-ss2012-all-md.md](tsql-appliesto-ss2012-all-md.md)]`  | [!INCLUDE[../includes/tsql-appliesto-ss2012-all-md.md](../includes/tsql-appliesto-ss2012-all-md.md)]  |
|   tsql-appliesto-ss2012-asdb-asdw-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md.md](../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md.md](../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]  |
|   tsql-appliesto-ss2012-asdbmi-xxxx-xxx-md.md |   `[!INCLUDE[tsql-appliesto-ss2012-asdbmi-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2012-asdbmi-xxxx-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2012-asdbmi-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2012-asdbmi-xxxx-xxx-md.md)]  |
|   tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]  |
|   tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md   |   `[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]  |
|   tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]  |
|   tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]  |
|   tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]  |
|   tsql-appliesto-ss2016-all-md.md |   `[!INCLUDE[tsql-appliesto-ss2016-all-md.md](tsql-appliesto-ss2016-all-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2016-all-md.md](../includes/tsql-appliesto-ss2016-all-md.md)]  |
|   tsql-appliesto-ss2016-asdb-asdw-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md.md](../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md.md](../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]  |
|   tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]  |
|   tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md   |   `[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md](../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md](../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]  |
|   tsql-appliesto-ss2016-xxxx-asdw-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-xxx-md.md](../includes/tsql-appliesto-ss2016-xxxx-asdw-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-xxx-md.md](../includes/tsql-appliesto-ss2016-xxxx-asdw-xxx-md.md)]  |
|   tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]  |
|   tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md   |   `[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]`  | [!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]  |
|   tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]  |
|   tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]  |
|   t-sql-appliesto-ss-asdbmi-xxxx-pwd-md.md    |   `[!INCLUDE[t-sql-appliesto-ss-asdbmi-xxxx-pwd-md.md](../includes/t-sql-appliesto-ss-asdbmi-xxxx-pwd-md.md)]`    | [!INCLUDE[t-sql-appliesto-ss-asdbmi-xxxx-pwd-md.md](../includes/t-sql-appliesto-ss-asdbmi-xxxx-pwd-md.md)]    |
|   tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md](../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md](../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]  |
|   tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md](../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]  |
|   tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md   |   `[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md](../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]`  | [!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md](../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]  |
|   tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md   |   `[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md](../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]`  | [!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md](../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]  |
|   tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md   |   `[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md](../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]`  | [!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md](../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]  |
|&nbsp; | &nbsp; | &nbsp; |  

## <a name="analysis-services-applies-to"></a>Analysis Services 적용 대상

| 파일 이름| Markdown 예제 |image|
| :-------------| :----------| :-------------------|
|   ssas-appliesto-sql2016.md   |   `[!INCLUDE[ssas-appliesto-sql2016.md](../includes/ssas-appliesto-sql2016.md)]`  | [!INCLUDE[ssas-appliesto-sql2016.md](../includes/ssas-appliesto-sql2016.md)]  |
|   ssas-appliesto-sql2016-later.md |   `[!INCLUDE[ssas-appliesto-sql2016-later.md](../includes/ssas-appliesto-sql2016-later.md)]`  | [!INCLUDE[ssas-appliesto-sql2016-later.md](../includes/ssas-appliesto-sql2016-later.md)]  |
|   ssas-appliesto-sql2016-later-aas.md |   `[!INCLUDE[ssas-appliesto-sql2016-later-aas.md](../includes/ssas-appliesto-sql2016-later-aas.md)]`  | [!INCLUDE[ssas-appliesto-sql2016-later-aas.md](../includes/ssas-appliesto-sql2016-later-aas.md)]  |
|   ssas-appliesto-sql2017.md   |   `[!INCLUDE[ssas-appliesto-sql2017.md](../includes/ssas-appliesto-sql2017.md)]`  | [!INCLUDE[ssas-appliesto-sql2017.md](../includes/ssas-appliesto-sql2017.md)]  |
|   ssas-appliesto-sql2017-later-aas.md |   `[!INCLUDE[ssas-appliesto-sql2017-later-aas.md](../includes/ssas-appliesto-sql2017-later-aas.md)]`  | [!INCLUDE[ssas-appliesto-sql2017-later-aas.md](../includes/ssas-appliesto-sql2017-later-aas.md)]  |
|   ssas-appliesto-sqlas.md |   `[!INCLUDE[ssas-appliesto-sqlas.md](../includes/ssas-appliesto-sqlas.md)]`  | [!INCLUDE[ssas-appliesto-sqlas.md](../includes/ssas-appliesto-sqlas.md)]  |
|   ssas-appliesto-sqlas-aas.md |   `[!INCLUDE[ssas-appliesto-sqlas-aas.md](../includes/ssas-appliesto-sqlas-aas.md)]`  | [!INCLUDE[ssas-appliesto-sqlas-aas.md](../includes/ssas-appliesto-sqlas-aas.md)]  |
|   ssas-appliesto-sqlas-all.md |   `[!INCLUDE[ssas-appliesto-sqlas-all.md](../includes/ssas-appliesto-sqlas-all.md)]`  | [!INCLUDE[ssas-appliesto-sqlas-all.md](../includes/ssas-appliesto-sqlas-all.md)]  |
|   ssas-appliesto-sqlas-all-aas.md |   `[!INCLUDE[ssas-appliesto-sqlas-all-aas.md](../includes/ssas-appliesto-sqlas-all-aas.md)]`  | [!INCLUDE[ssas-appliesto-sqlas-all-aas.md](../includes/ssas-appliesto-sqlas-all-aas.md)]  |
|&nbsp; | &nbsp; | &nbsp; |  

## <a name="reporting-services-applies-to"></a>Reporting Services 적용 대상

| 파일 이름| Markdown 예제 |image|
| :-------------| :----------| :-------------------|
|   ssrs-appliesto-2017-and-later.md    |   `[!INCLUDE[ssrs-appliesto-2017-and-later.md](../includes/ssrs-appliesto-2017-and-later.md)]`    | [!INCLUDE[ssrs-appliesto-2017-and-later.md](../includes/ssrs-appliesto-2017-and-later.md)]    |
|   ssrs-appliesto-not-pbirs.md |   `[!INCLUDE[ssrs-appliesto-not-pbirs.md](../includes/ssrs-appliesto-not-pbirs.md)]`  | [!INCLUDE[ssrs-appliesto-not-pbirs.md](../includes/ssrs-appliesto-not-pbirs.md)]  |
|   ssrs-appliesto-pbirs.md |   `[!INCLUDE[ssrs-appliesto-pbirs.md](../includes/ssrs-appliesto-pbirs.md)]`  | [!INCLUDE[ssrs-appliesto-pbirs.md](../includes/ssrs-appliesto-pbirs.md)]  |
|   ssrs-appliesto-sharepoint-2013-2016.md  |   `[!INCLUDE[ssrs-appliesto-sharepoint-2013-2016.md](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]`    | [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016.md](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]    |
|   ssrs-appliesto-sql2016-preview.md   |   `[!INCLUDE[ssrs-appliesto-sql2016-preview.md](../includes/ssrs-appliesto-sql2016-preview.md)]`  | [!INCLUDE[ssrs-appliesto-sql2016-preview.md](../includes/ssrs-appliesto-sql2016-preview.md)]  |
|&nbsp; | &nbsp; | &nbsp; |  