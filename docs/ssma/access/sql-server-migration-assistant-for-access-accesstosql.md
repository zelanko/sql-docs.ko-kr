---
title: 액세스 SQL Server Migration Assistant (AccessToSQL) | Microsoft Docs
description: Access 용 SSMA에 대해 알아보고 Access 데이터베이스를 SQL Server 또는 Azure SQL Database로 마이그레이션하기 위한 단계별 지침을 따르세요.
ms.prod: sql
ms.custom: ''
ms.date: 10/10/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 40c1eb02-26b2-44ba-969d-6c430c61c281
author: Jtoland
ms.author: Jtoland
manager: murato
ms.openlocfilehash: 2e4ce80a111efcf978da55cab280205b08acdd1f
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84292948"
---
# <a name="sql-server-migration-assistant-for-access-accesstosql"></a>액세스 SQL Server Migration Assistant (AccessToSQL)

[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Access 용 SSMA (Migration Assistant)는 데이터베이스 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 를 마이그레이션하는 데 사용 되는 도구입니다. 97 ~ 2010 버전에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 On windows 및 linux, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2019 on windows 및 linux 또는 Azure SQL Database에 액세스 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 합니다. Access 용 SSMA는 Access 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL database 개체로 변환 하 고, 이러한 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL Database 로드 한 다음 access에서 또는 Azure SQL Database로 데이터를 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
이 설명서에서는 액세스용 SSMA를 소개 하 고 Access 데이터베이스 Azure SQL Database를로 마이그레이션하는 방법에 대 한 단계별 지침 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션 후 발생할 수 있는 문제에 대 한 정보를 제공 합니다.  
  
## <a name="contents"></a>콘텐츠  
  
|섹션|설명|
|-----------|---------------|
|[Access용 SSMA의 새로운 기능](https://msdn.microsoft.com/a24d3fc0-6911-4bfa-828a-197abf222e02)|SSMA 릴리스에 대 한 변경 내용을 나열 합니다.|  
|[액세스용 SQL Server Migration Assistant 설치](installing-sql-server-migration-assistant-for-access-accesstosql.md)|SSMA를 설치 하기 위한 필수 구성 요소, SSMA 설치 및 라이선스 절차 및 최신 버전에 대 한 링크를 나열 합니다.|  
|[Access &#40;AccessToSQL&#41;에 대 한 SQL Server Migration Assistant 시작](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)|SSMA 및 해당 사용자 인터페이스를 소개 합니다.|  
|[마이그레이션을 위해 Access 데이터베이스 준비](preparing-access-databases-for-migration-accesstosql.md)|/Sql Azure로의 변환을 위해 Access 데이터베이스를 준비 하는 방법을 설명 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)|변환 프로세스에 대 한 개요와 프로세스의 각 단계에 대 한 자세한 정보를 제공 합니다.|  
|[SQL Server에 액세스 응용 프로그램 연결](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)|에서 기존 Access 응용 프로그램을 사용 하는 방법을 설명 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[사용자 인터페이스 참조](user-interface-reference-accesstosql.md)|SSMA 대화 상자에 대 한 설명서가 포함 되어 있습니다.|  
|[Access용 SSMA 콘솔 작업](working-with-ssma-for-access-console-accesstosql.md)|SSMA 콘솔 응용 프로그램에 대 한 설명서가 포함 되어 있습니다.|  
|[Access에 대 한 SSMA 지원 받기](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|추가 지원을 받는 방법에 대 한 정보를 제공 합니다.|  
