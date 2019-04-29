---
title: 데이터베이스 메일 외부 프로그램 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- external programs [Database Mail]
- DatabaseMail90.exe
- Database Mail [SQL Server], external programs
ms.assetid: bc124164-eb6e-4b7f-bf66-98a3113d02f7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6c617e4f7c069a869935fa4ed83d28c02d0b0b9a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62917644"
---
# <a name="database-mail-external-program"></a>데이터베이스 메일 외부 프로그램
  데이터베이스 메일 외부 프로그램의 실행 파일은 **DatabaseMail.exe**이며 **설치 위치의** MSSQL\Binn 디렉터리 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 들어 있습니다. 데이터베이스 메일은 처리할 전자 메일 메시지가 있는 경우 Service Broker 활성화를 사용하여 외부 프로그램을 시작합니다. 데이터베이스 메일은 외부 프로그램의 인스턴스 하나를 시작합니다. 외부 프로그램은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 서비스 계정의 보안 컨텍스트에서 실행됩니다.  
  
 **항목 내용:**  
  
-   [데이터베이스 메일 외부 프로그램 개념](#ComponentsAndConcepts)  
  
-   [데이터베이스 메일 외부 프로그램 구성 관련 태스크](#RelatedTasks)  
  
##  <a name="ComponentsAndConcepts"></a> 데이터베이스 메일 외부 프로그램 개념  
 외부 프로그램이 시작되면 이 프로그램은 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 전자 메일 메시지를 처리하기 시작합니다. 지정된 제한 시간 동안 보낼 메시지가 없는 경우 프로그램이 종료됩니다. 데이터베이스 메일 구성 마법사 또는 데이터베이스 메일 저장 프로시저를 사용하여 프로그램의 종료 대기 시간을 구성할 수 있습니다. 자세한 내용은 [sysmail_configure_sp&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql)에 대한 서비스 계정의 보안 컨텍스트에서 실행됩니다.  
  
 외부 프로그램은 **msdb** 데이터베이스의 시스템 테이블에 정보를 저장합니다. 외부 프로그램이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 통신할 수 없는 경우 프로그램은 Microsoft Windows 애플리케이션 이벤트 로그에 오류를 기록합니다. **데이터베이스 메일 구성 마법사** 의 **시스템 매개 변수 구성** 대화 상자에서 로깅 수준이 **자세히**로 설정되어 있으면 추가 메시지 로깅이 제공됩니다.  
  
 외부 프로그램은 효율적인 처리를 위해 계정 및 프로필 정보를 캐시한다는 점에 유의하세요. 그러므로 계정 및 프로필에 대한 구성 변경 내용은 몇 분 동안 외부 프로그램에 반영되지 않을 수 있습니다.  
  
##  <a name="RelatedTasks"></a> 데이터베이스 메일 외부 프로그램 구성 관련 태스크  
  
|구성 태스크|항목 링크|  
|------------------------|----------------|  
|외부 프로그램을 종료하기 전에 시간을 지정합니다.|[sysmail_configure_sp&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql)|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [데이터베이스 메일 로그 및 감사](database-mail-log-and-audits.md)   
 [데이터베이스 메일](database-mail.md)  
  
  
