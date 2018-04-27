---
title: SSMA는 MySQL 구성 요소 (MySQLToSql)에 대 한 제거 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a62a3f9a3fdb5e6876cb6ac27d4f9f1fb2500cc5
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>SSMA는 MySQL 구성 요소 (MySQLToSql)에 대 한 제거
완료 했을 때에 mysql 데이터베이스를 마이그레이션 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA 구성 요소를 제거 해야 할 경우가 있습니다. 언제 든 지 클라이언트 구성 요소를 제거할 수 있습니다. 그러나 확장 팩을 제거 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , 그런 다음 SSMA는 더 이상 지원 데이터에서 MySQL 서버 쪽 데이터 마이그레이션 엔진을 사용 하 여 대상 데이터베이스 (SQL Server/SQL Azure)에 마이그레이션.  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>SSMA는 MySQL 클라이언트에 대 한 제거  
SSMA를 사용 하 여 제거할 수 있습니다 **프로그램 추가 / 제거**합니다.  
  
**SSMA를 제거 하려면**  
  
1.  제어판을 열고 **프로그램 추가 / 제거**합니다.  
  
2.  선택 **Microsoft SQL Server Migration Assistant for MySQL**, 클릭 하 고 **제거**합니다.  
  
3.  확인 하려면 SSMA를 제거 하려면 클릭 하십시오 **예**합니다.  
  
## <a name="uninstalling-the-extension-pack"></a>확장 팩을 제거  
사용 하 여 확장 팩을 제거할 수 **프로그램 추가 / 제거**합니다.  
  
**확장 팩을 제거 하려면**  
  
1.  제어판을 열고 **프로그램 추가 / 제거**합니다.  
  
2.  선택 **Microsoft SQL Server Migration Assistant for MySQL 확장 팩**, 클릭 하 고 **제거**합니다.  
  
3.  확인 하려면 확장 팩을 제거 하려면 클릭 하십시오 **예**합니다.  
  
4.  인스턴스에서 데이터베이스 스크립트 유틸리티 페이지와 인스턴스를 선택 하 고 클릭 **다음**합니다.  
  
5.  연결 매개 변수 페이지에서 인증 방법을 선택 하 고 클릭 **다음**합니다.  
  
    Windows 인증 Windows 자격 증명을 사용 하 여 인스턴스의에 로그온 하려고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 입력 해야 인증을 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 로그인 이름 및 암호.  
  
6.  작업이 완료 페이지에서 클릭 **확인**합니다.  
  
7.  완료 페이지에서 클릭 **종료**합니다.  
  
제거 프로세스가 완료 된 후의 개체를 확인할 수 있습니다는 **sysdb.ssma_MySQL** 스키마 및 전체 **sysdb** , 데이터베이스를 사용 하 여 제거 된 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]합니다. 그러나 다른 SSMA 제품을 사용 하는 경우 사용 된 **sysdb** 데이터베이스입니다. 데이터베이스가 존재 하는 경우이 데이터베이스의 개체에 없는 다른 데이터베이스 참조 하는지 확인 했으면 데이터베이스를 분리할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
[SSMA MySQL 클라이언트에 대 한 설치 &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[SQL Server에 SSMA 구성 요소 설치](http://msdn.microsoft.com/en-us/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
