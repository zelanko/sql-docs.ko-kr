---
title: "Access 데이터베이스 마이그레이션 (AccessToSQL)에 대 한 준비 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access databases, versions
- Access databases, when to migrate
- Access databases, workgroup security
- backing up databases
- documenting databases
- files, preparing
- migrating databases, versions
- migrating databases, when to migrate
- versions of Access
- workgroup security
ms.assetid: 9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114
caps.latest.revision: 20
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8319115ed2da6500644c89d513c1e44d3fb11825
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>Access 데이터베이스 마이그레이션 (AccessToSQL) 준비
Access 데이터베이스를 마이그레이션하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 어떤 데이터베이스를 마이그레이션하려면 결정 해야 절과 다음 있는지 확인 하십시오 해당 데이터베이스 마이그레이션에 대해 준비 합니다.  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>SQL Server로 마이그레이션 시기 결정  
액세스 데이터베이스 엔진으로 사용 되는 Jet 데이터베이스 엔진에는 데이터 관리를 위한 유연 하 고 사용 하기 쉬운 솔루션입니다. 그러나 데이터베이스 크기가 커질 및 더 많은 업무용으로 많은 사용자가 찾을 더 큰 성능, 보안 또는 가용성 필요가 없다고. 보다 강력한 데이터 플랫폼을 필요로 하는 응용 프로그램의 경우 해당 응용 프로그램에 대 한 기본 데이터베이스 이동 고려 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 마이그레이션 시기를 결정 하는 방법에 대 한 자세한 내용은 참조는 [마이그레이션 정보 페이지](http://go.microsoft.com/fwlink/?LinkId=68571) 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 웹 사이트입니다.  
  
데이터베이스를 마이그레이션한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]계속 연결 된 테이블을 사용 하 여 액세스를 사용할 수 있습니다, 또는 응용 프로그램을 수동으로 마이그레이션할 수 있습니다 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 와 직접 상호 작용 하는.NET Framework 기반 코드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
## <a name="determining-which-databases-to-migrate"></a>마이그레이션할 데이터베이스를 결정 합니다.  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) 액세스를 위해 사용자에 대 한 Access 데이터베이스를 찾을 수 있습니다. 그런 다음 해당 데이터베이스에 대 한 메타 데이터를 내보낼 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 내보내기 및 메타 데이터를 쿼리 하는 방법에 대 한 자세한 내용은 참조 [액세스 인벤토리 내보내기](http://msdn.microsoft.com/en-us/7e1941fb-3d14-4265-aff6-c77a4026d0ed)합니다.  
  
**참고** 에서 지 원하는 모든 액세스 기능 및 설정 또는로 쉽게 변환할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 데이터베이스를 마이그레이션하기 전에 참조 [호환 되지 않는 기능 액세스](http://msdn.microsoft.com/en-us/99d45b9c-e3b9-4d56-8c25-b594b887ace1)합니다.  
  
## <a name="preparing-for-migration"></a>마이그레이션을 준비  
로 마이그레이션하기 위해 Access 데이터베이스를 준비 하려면 다음 지침을 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
### <a name="upgrading-older-access-databases"></a>오래 된 Access 데이터베이스를 업그레이드합니다.  
Access 용 SSMA는 Access 97 및 이상 버전을 지원합니다. 이전 버전의 데이터베이스를 액세스 하는 경우 열고 Access 97 또는 이후 버전에서 데이터베이스를 저장 합니다.  
  
### <a name="removing-workgroup-protection"></a>작업 그룹 보호 제거  
SSMA는 작업 그룹 보호를 사용 하는 데이터베이스를 마이그레이션할 수 없습니다. Access 데이터베이스에서 작업 그룹 보호를 제거 하려면 다음을 수행할 수 있습니다.  
  
1.  Access 데이터베이스 파일을 다른 위치로 복사 합니다.  
  
2.  복사 된 데이터베이스를 엽니다.  
  
3.  에 **도구** 메뉴에서 **보안**를 선택한 후 **사용자 및 그룹 권한**합니다.  
  
4.  선택은 **사용자** 옵션을 선택는 **관리자** 사용자, 다음 되어 있는지 확인는 **관리** 권한이 선택 됩니다.  
  
5.  선택 된 **그룹** 옵션을 선택는 **사용자** 를 그룹화 하 고 다음 사항을 확인 하십시오는 **관리** 권한이 선택 됩니다.  
  
6.  클릭 **확인**, 선택한 다음는 **파일** 메뉴를 클릭 하 여 **종료**합니다.  
  
이제 복사 된 데이터베이스를 마이그레이션할 SSMA를 사용할 수 있습니다. 스키마를 로드 한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 수동으로 보안을 유지할 수는 데이터베이스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
### <a name="backing-up-databases"></a>데이터베이스 백업  
Access 데이터베이스를 마이그레이션하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]를 마이그레이션하는 경우는 Access 데이터베이스를 백업 해야 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 마이그레이션합니다는 데이터베이스 개체 및 데이터에 액세스 합니다.  
  
Access 데이터베이스를 백업 하는 **도구** 메뉴에서 **데이터베이스 유틸리티**를 선택한 후 **데이터베이스 백업**합니다.  
  
백업 하는 방법에 대 한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 참조 "Backing Up and Restoring Databases에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
### <a name="documenting-databases"></a>데이터베이스 문서화  
Access 데이터베이스, 데이터베이스 개체, 파일 크기 및 사용 권한 목록 등의 문서 속성을 수도 있습니다. Access에서는이 문서에서 생성 하는 **도구** 메뉴에서 **분석**, 클릭 하 고 **데이터베이스 구조**합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[SQL Server에 대 한 액세스 응용 프로그램 연결](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4)  
  

