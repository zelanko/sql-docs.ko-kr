---
title: SQL Server Migration Assistant for Access (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 08/14/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 40c1eb02-26b2-44ba-969d-6c430c61c281
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: On Demand
ms.openlocfilehash: a9634591b3f9d1c75bc64e89c363a38e4d6b1b7e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-migration-assistant-for-access-accesstosql"></a>SQL Server Migration Assistant for Access (AccessToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) 액세스에는 마이그레이션에 대 한 도구에서 데이터베이스 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 97 2010과 버전에 액세스 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Windows 및 Linux (미리 보기)에서 2017 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] Azure SQL DB입니다. Access 용 SSMA는 Access 데이터베이스 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스 개체를 로드 하는 것에 개체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터에 대 한 액세스를 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 합니다.  
  
이 설명서에서는 Access 용 SSMA를 소개 하 고 액세스 데이터베이스 마이그레이션에 대 한 단계별 지침을 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure와 마이그레이션 후 발생할 수 있는 문제에 대 한 정보입니다.  
  
## <a name="contents"></a>내용  
  
|섹션|Description|  
|-----------|---------------|  
|[Access용 SSMA의 새로운 기능](http://msdn.microsoft.com/en-us/a24d3fc0-6911-4bfa-828a-197abf222e02)|SSMA 릴리스에 변경 내용을 나열합니다.|  
|[SQL Server Migration Assistant for Access 설치](http://msdn.microsoft.com/en-us/dd50eebd-75df-4e0d-8c4d-88b511aae4c7)|SSMA를 설치 하 고 최신 버전에 대 한 링크 및 SSMA를 라이선스 하는 절차를 설치 하기 위한 필수 구성 요소를 나열 합니다.|  
|[Getting Started with SQL Server Migration Assistant for Access &#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)|SSMA와 사용자 인터페이스를 소개합니다.|  
|[Access 데이터베이스 마이그레이션을 준비](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)|변환에 대해 Access 데이터베이스를 준비 하는 방법에 설명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SQL Azure입니다.|  
|[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)|프로세스의 각 단계에 대 한 자세한 정보 및 변환 프로세스의 개요를 제공합니다.|  
|[SQL Server에 대 한 액세스 응용 프로그램 연결](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4)|기존 Access 응용 프로그램을 사용 하는 방법에 설명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.|  
|[사용자 인터페이스 참조](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)|SSMA 대화 상자에 대 한 설명서를 포함합니다.|  
|[Access용 SSMA 콘솔 작업](http://msdn.microsoft.com/en-us/ef94e843-9f88-45a2-86c4-a0af268738c4)|SSMA 콘솔 응용 프로그램에 대 한 설명서를 포함 합니다.|  
|[액세스용 SSMA 지원 받기](http://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|추가 도움말에 대 한 정보를 제공 합니다.|  
  
