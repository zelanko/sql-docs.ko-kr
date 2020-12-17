---
title: 명령줄 도구를 사용하여 프로젝트 기반 데이터베이스 개발
description: 'SQL Server Data Tools가 .dacpac 파일을 사용할 수 있도록 제공하는 명령줄 도구(예: SQLPackage.exe 및 dbSqlPackage)에 대한 사용 가능한 리소스를 살펴봅니다.'
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 9a26def9-8fbd-43e4-9e57-414840b73ed8
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 04/26/2017
ms.openlocfilehash: f84638d0ded57fcc1312258422de522aec997b39
ms.sourcegitcommit: 866554663ca3191748b6e4eb4d8d82fa58c4e426
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97559245"
---
# <a name="project-oriented-database-development-using-command-line-tools"></a>명령줄 도구를 사용하여 프로젝트 기반 데이터베이스 개발

SQL Server Data Tools는 많은 프로젝트 기반 데이터베이스 개발 시나리오를 활성화하는 명령줄 도구입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|-|-|  
|[SqlPackage.exe](../tools/sqlpackage/sqlpackage.md)|이 항목에서는 다음 작업에 사용하는 SQLPackage.exe 유틸리티에 대해 설명합니다.<br /><br />- 라이브 SQL Server 데이터베이스에서 .dacpac 파일을 추출합니다.<br />- .dacpac 파일을 라이브 SQL Server 데이터베이스에 게시하여 .dacpac와 일치하도록 라이브 데이터베이스 스키마를 증분식으로 업데이트합니다.<br />- .dacpac 파일을 라이브 SQL Server 데이터베이스와 비교하고 라이브 데이터베이스를 업데이트하지 않고 증분 업그레이드 Transact\-SQL 스크립트를 생성합니다.<br />- 두 .dacpac 파일을 비교하여 증분 업그레이드 Transact\-SQL 스크립트를 생성합니다.<br />- 데이터베이스가 증분식으로 업그레이드된 경우 발생하는 증분 업그레이드 변경을 요약하는 XML 보고서를 생성합니다.|  
|[dbSqlPackage 공급자와 함께 MSDeploy 사용](../ssdt/using-msdeploy-with-dbsqlpackage-provider.md)|이 항목에서는 SSDT에 포함된 dbSqlPackage라는 [웹 배포 도구](https://go.microsoft.com/fwlink/?LinkId=231798) 공급자에 대해 설명합니다. 이 공급자는 Microsoft IIS(인터넷 정보 서비스) 웹 배포 도구(MSDeploy.exe)와 함께 작동하며 다음 작업에 사용합니다.<br /><br />- 원격/로컬 SQL Server 또는 Azure SQL 데이터베이스에서 .dacpac 파일을 추출합니다.<br />- .dacpac 파일을 원격/로컬 SQL Server 또는 Azure SQL 데이터베이스에 게시하여 증분식으로 업그레이드합니다.<br />- 로컬 SQL Server 데이터베이스에서 원격 SQL Server 또는 Azure SQL 데이터베이스에 게시하여 원격 데이터베이스를 증분식으로 업그레이드합니다.<br />- .dacpac을 원격/로컬 SQL Server 또는 Azure SQL 데이터베이스와 비교하여 라이브 데이터베이스를 업데이트하지 않고 증분 업그레이드 Transact\-SQL 스크립트를 생성합니다.<br />- 데이터베이스가 증분식으로 업그레이드된 경우 발생하는 증분 업그레이드 변경을 요약하는 XML 보고서를 생성합니다.|  
  
## <a name="related-sections"></a>관련 섹션  
[프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md)  
  
