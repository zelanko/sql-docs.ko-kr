---
description: MySQL용 SSMA 구성 요소 제거(MySQLToSql)
title: MySQL 용 SSMA 구성 요소 제거 (MySQLToSql) | Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3a7932d79c414fb79dfc29074c1b8a5888c85827
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418509"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>MySQL용 SSMA 구성 요소 제거(MySQLToSql)
MySQL에서로 데이터베이스 마이그레이션을 마치면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA 구성 요소를 제거 하는 것이 좋습니다. 언제 든 지 클라이언트 구성 요소를 제거할 수 있습니다. 그러나에서 확장 팩을 제거 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA에서 서버 쪽 데이터 마이그레이션 엔진을 사용 하 여 MySQL에서 대상 데이터베이스로의 데이터 마이그레이션 (SQL Server/SQL Azure)을 더 이상 지원 하지 않습니다.  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>MySQL 용 SSMA 클라이언트 제거  
**프로그램 추가/제거**를 사용 하 여 ssma를 제거할 수 있습니다.  
  
**SSMA를 제거 하려면**  
  
1.  제어판에서 **프로그램 추가 또는 제거**를 엽니다.  
  
2.  **MySQL에 Microsoft SQL Server Migration Assistant**을 선택 하 고 **제거**를 클릭 합니다.  
  
3.  SSMA를 제거할 것인지 확인 하려면 **예**를 클릭 합니다.  
  
## <a name="uninstalling-the-extension-pack"></a>확장 팩 제거  
**프로그램 추가/제거**를 사용 하 여 확장 팩을 제거할 수 있습니다.  
  
**확장 팩을 제거 하려면**  
  
1.  제어판에서 **프로그램 추가 또는 제거**를 엽니다.  
  
2.  **MySQL 확장 팩의 Microsoft SQL Server Migration Assistant**을 선택 하 고 **제거**를 클릭 합니다.  
  
3.  확장 팩을 제거할 것인지 확인 하려면 **예**를 클릭 합니다.  
  
4.  유틸리티 데이터베이스 스크립트를 사용 하는 인스턴스 페이지에서 인스턴스를 선택 하 고 **다음**을 클릭 합니다.  
  
5.  연결 매개 변수 페이지에서 인증 방법을 선택 하 고 **다음**을 클릭 합니다.  
  
    Windows 인증에서는 Windows 자격 증명을 사용 하 여 인스턴스에 로그온을 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인증을 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 이름 및 암호를 입력 해야 합니다.  
  
6.  작업 완료 페이지에서 **확인**을 클릭 합니다.  
  
7.  마침 페이지에서 **끝내기**를 클릭 합니다.  
  
제거 프로세스가 완료 된 후에는를 사용 하 여 **sysdb. ssma_MySQL** 스키마의 개체와 전체 **sysdb** 데이터베이스가 제거 되었는지 확인할 수 있습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . 그러나 다른 SSMA 제품을 사용 하는 경우 **sysdb** 데이터베이스도 사용 합니다. 데이터베이스가 존재 하 고이 데이터베이스의 개체를 참조 하는 다른 데이터베이스가 없는 경우 데이터베이스를 분리할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[MySQLToSQL&#41;&#40;MySQL 용 SSMA 클라이언트 설치 ](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[SQL Server에 SSMA 구성 요소 설치](installing-ssma-components-on-sql-server-mysqltosql.md)  
  
