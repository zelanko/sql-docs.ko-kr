---
title: Sybase 용 SQL Server Migration Assistant (SybaseToSQL) | Microsoft Docs
description: Sybase 용 SSMA에 대해 알아보고 ASE 데이터베이스를 SQL Server 또는 Azure SQL Database로 마이그레이션하기 위한 단계별 지침을 따르세요.
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 59e63eac-8a7e-4d54-be1c-0633a9bf510d
author: Jtoland
ms.author: Jtoland
manager: murato
ms.openlocfilehash: 269fa36b578b7b13d12d5b6fd9645e84c7c39244
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293991"
---
# <a name="sql-server-migration-assistant-for-sybase-sybasetosql"></a>Sybase 용 SQL Server Migration Assistant (SybaseToSQL)

[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SYBASE ase (Sybase Server Enterprise) 용 SSMA (Migration Assistant)는 ase 데이터베이스를로 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션하기 위한 도구입니다. Windows 및 linux에서 2012, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] windows 및 linux의 2019 또는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Azure SQL Database입니다. Sybase 용 SSMA는 ASE 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체로 변환 하 고, 이러한 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL Database 만든 다음 ASE에서 또는 Azure SQL Database로 데이터를 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
이 설명서에서는 Sybase 용 SSMA를 소개 하 고 ASE 데이터베이스 Azure SQL Database를로 마이그레이션하는 방법에 대 한 단계별 지침 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션 후 발생할 수 있는 문제에 대 한 정보를 제공 합니다. 자세히 알아보려면 다음 문서를 참조 하세요.  
  
## <a name="contents"></a>콘텐츠  
  
|섹션|설명|
|-----------|---------------|
|[Sybase 용 SSMA의 새로운 기능 &#40;SybaseToSQL&#41;](../../ssma/sybase/what-s-new-in-ssma-for-sybase-sybasetosql.md)|SSMA 릴리스에 대 한 변경 내용을 나열 합니다.|  
|[Sybase 용 SSMA &#40;SybaseToSQL&#41;설치](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)|인스턴스를 실행 하는 컴퓨터에 Sybase 클라이언트 및 필수 구성 요소에 대 한 SSMA를 설치 하기 위한 필수 구성 요소 및 지침을 제공 하는 문서가 포함 되어 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Sybase &#40;SybaseToSQL&#41;용 SSMA 시작](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)|사용자 인터페이스, 프로젝트 및 구성 옵션을 소개 합니다.|  
|[Sybase ASE 데이터베이스를 SQL Server로 마이그레이션-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)|변환 프로세스에 대 한 개요와 프로세스의 각 단계에 대 한 자세한 정보를 제공 합니다.|  
|[사용자 인터페이스 참조 &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)|Sybase 용 SSMA 대화 상자에 대 한 설명서가 포함 되어 있습니다.|  
|[Sybase용 SSMA 콘솔 작업](working-with-ssma-for-sybase-console-sybasetosql.md)|SSMA 콘솔 응용 프로그램에 대 한 설명서가 포함 되어 있습니다.|  
|[Sybase 지원을 위한 SSMA 가져오기](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|추가 지원을 받는 방법에 대 한 정보를 제공 합니다.|  
