---
title: SQL Server 오류 로그 보기
description: 현재 오류 로그 또는 이전 로그 백업을 보고 SQL Server에서 발생하는 문제를 검색하여 프로세스가 성공적으로 완료되었는지 확인할 수 있습니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- cycling SQL Server error log
- viewing SQL Server error log
- errors [SQL Server], logs
- SQL Server error log
- displaying SQL Server error log
- logs [SQL Server], SQL Server error logs
ms.assetid: 6908c21a-65e3-458f-a272-fee256d86448
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 149ece24923ad8f4b46f9d24f9e6568d05960cec
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463724"
---
# <a name="viewing-the-sql-server-error-log"></a>SQL Server 오류 로그 보기
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그를 보면 프로세스(예: 백업 및 복원 작업, 일괄 처리 명령, 다른 스크립트 및 프로세스)가 성공적으로 완료되었는지 확인할 수 있습니다. 이것은 자동 복구 메시지(특히 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 중지되었다가 다시 시작된 경우), 커널 메시지 또는 기타 서버 수준 오류 메시지 등의 현재 또는 잠재적 문제 영역을 찾아내는 데 유용합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 텍스트 편집기를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 오류 로그를 봅니다. 오류 로그를 보는 방법은 [Open Log File Viewer](../../relational-databases/logs/open-log-file-viewer.md)를 참조하십시오. 기본적으로 오류 로그는 `Program Files\Microsoft SQL Server\MSSQL.`*n*`\MSSQL\LOG\ERRORLOG` 및 `ERRORLOG.`*n* 파일에 있습니다.  
  
 새 오류 로그는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 시작할 때마다 만들어지지만 [sp_cycle_errorlog](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md) 시스템 저장 프로시저를 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 다시 시작하지 않아도 오류 로그 파일을 반복할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 대개 이전 여섯 개의 로그에 대한 백업을 포함하며 로그 백업에 가장 최근에 사용한 순서대로 .1, .2,…와 같은 방식으로 확장명을 부여합니다. 현재 오류 로그에는 확장명이 없습니다.  
  
 오프라인 상태이거나 시작할 수 없는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그를 확인할 수도 있습니다. 자세한 내용은 [오프라인 로그 파일 보기](../../relational-databases/logs/view-offline-log-files.md)를 참조하세요.  
  
  
