---
title: DB2 용 SQL Server Migration Assistant (DB2ToSQL) | Microsoft Docs
description: D b 2 용 SSMA에 대해 알아보고 DB2 데이터베이스를 SQL Server 또는 Azure SQL Database로 마이그레이션하기 위한 단계별 지침을 따르세요.
ms.prod: sql
ms.custom: ''
ms.date: 10/10/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7633f631-ffad-469a-8441-8831a6a9f932
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 6ade3ce31bed08bdb7b25b09ec0d5bbcf91405f1
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936514"
---
# <a name="sql-server-migration-assistant-for-db2-db2tosql"></a>DB2 용 SQL Server Migration Assistant (DB2ToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)]D b 2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 용 SSMA (Migration Assistant)는 db2 데이터베이스를로 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션하기 위한 도구입니다. Windows 및 linux에서 2012, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] windows 및 linux의 2019 또는 Azure SQL Database입니다. D b 2 용 SSMA는 DB2 데이터베이스 개체를 데이터베이스 개체로 변환 하 고, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 해당 개체를 만든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 후 DB2에서 또는 Azure SQL Database로 데이터를 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
이 설명서에서는 d b 2 용 SSMA를 소개 하 고 DB2 데이터베이스를로 마이그레이션하는 방법에 대 한 단계별 지침을 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 다음 표에서는 자세한 정보를 확인할 수 있는 문서를 보여 줍니다.  
  
## <a name="contents"></a>콘텐츠  
  
|섹션|Description|  
|-----------|---------------|
|[DB2용 SSMA의 새로운 기능](https://msdn.microsoft.com/1cc38f85-3caa-42d0-8c76-a380c1d15c67)|D b 2 용 SSMA 버전의 새로운 기능|  
|[DB2ToSQL&#41;&#40;DB2 용 SSMA 클라이언트 설치](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)|을 실행 하는 컴퓨터에서 DB2 용 SSMA 클라이언트 및 필수 구성 요소를 설치 하기 위한 필수 구성 요소 및 지침을 제공 하는 문서가 포함 되어 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[D b 2 용 SSMA &#40;DB2ToSQL&#41;시작](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)|사용자 인터페이스, 프로젝트 및 구성 옵션을 소개 합니다.|  
|[DB2 데이터베이스를 SQL Server &#40;DB2ToSQL&#41;로 마이그레이션](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)|변환 프로세스에 대 한 개요와 프로세스의 각 단계에 대 한 자세한 정보를 제공 합니다.|  
|[DB2ToSQL&#41;&#40;사용자 인터페이스 참조](../../ssma/db2/user-interface-reference-db2tosql.md)|DB2 용 SSMA 대화 상자에 대 한 설명서가 포함 되어 있습니다.|  
|[DB2 용 SSMA 콘솔 작업](https://msdn.microsoft.com/29d8787c-632e-4ff7-9ccc-3f7ad40480ec)|SSMA 콘솔 응용 프로그램에 대 한 설명서가 포함 되어 있습니다.|  
|[DB2 용 SSMA 지원 받기](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|추가 지원을 받는 방법에 대 한 정보를 제공 합니다.|  
