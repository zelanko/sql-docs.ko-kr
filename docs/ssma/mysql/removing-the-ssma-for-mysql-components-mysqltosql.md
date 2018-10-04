---
title: SSMA MySQL 구성 요소 (MySQLToSql)에 대 한 제거 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ad23c4add9b6e7ea9999a434261a95282f129935
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47604852"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>MySQL용 SSMA 구성 요소 제거(MySQLToSql)
완료 한 후에 mysql 데이터베이스 마이그레이션 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA 구성 요소를 제거 하는 것이 좋습니다. 언제 든 지 클라이언트 구성 요소를 제거할 수 있습니다. 그러나에서 확장 팩을 제거 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 그런 다음 SSMA는 더 이상 지원 MySQL에서 서버 쪽 데이터 마이그레이션 엔진을 사용 하 여 대상 데이터베이스 (SQL Server/SQL Azure)로 데이터 마이그레이션.  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>SSMA MySQL 클라이언트에 대 한 제거  
SSMA를 사용 하 여 제거할 수 있습니다 **프로그램 추가 / 제거**합니다.  
  
**SSMA를 제거 하려면**  
  
1.  제어판에서 엽니다 **프로그램 추가 / 제거**합니다.  
  
2.  선택 **Microsoft SQL Server Migration Assistant for MySQL**를 클릭 하 고 **제거**합니다.  
  
3.  확인 하려면 SSMA를 제거 하려면 클릭 하십시오 **예**합니다.  
  
## <a name="uninstalling-the-extension-pack"></a>확장 팩을 제거  
사용 하 여 확장 팩을 제거할 수 있습니다 **프로그램 추가 / 제거**합니다.  
  
**확장 팩을 제거 하려면**  
  
1.  제어판에서 엽니다 **프로그램 추가 / 제거**합니다.  
  
2.  선택 **Microsoft SQL Server Migration Assistant for MySQL 확장 팩**를 클릭 하 고 **제거**합니다.  
  
3.  확인 하려면 확장 팩을 제거 하려면 클릭 하십시오 **예**합니다.  
  
4.  인스턴스에서 유틸리티 데이터베이스 스크립트 페이지를 사용 하 여 인스턴스를 선택 하 고 클릭 **다음**합니다.  
  
5.  연결 매개 변수 페이지에서 인증 방법을 선택 하 고 클릭 **다음**합니다.  
  
    Windows 인증 Windows 자격 증명을 사용 하 여 인스턴스의 로그온 하려고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 입력 해야 인증을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 이름 및 암호입니다.  
  
6.  작업이 완료 페이지에서 클릭 **확인**합니다.  
  
7.  마침 페이지에서 클릭 **종료**합니다.  
  
제거 프로세스가 완료 되 면 개체는 확인할 수 있습니다 합니다 **sysdb.ssma_MySQL** 스키마 및 전체 **sysdb** 데이터베이스를 사용 하 여 제거 되었습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다. 그러나 다른 SSMA 제품을 사용 하는 경우도 사용 합니다 **sysdb** 데이터베이스입니다. 데이터베이스 존재 하 고이 데이터베이스의 개체에 없는 다른 데이터베이스 참조는 확신을 하는 경우에 데이터베이스를 분리할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
[SSMA MySQL 클라이언트에 대 한 설치 &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[SQL Server에 SSMA 구성 요소 설치](installing-ssma-components-on-sql-server-mysqltosql.md)  
  
