---
title: SQL Server Compact Edition 연결 관리자 편집기 (모든 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlmobileconnection.all.f1
helpviewer_keywords:
- SQL Server Compact Connection Manager Editor
ms.assetid: f9fbff4b-c502-44b3-8e7b-398d66e82206
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9e6b326e86e1a9e21a740c3bf1bd1fedb6919e98
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84962749"
---
# <a name="sql-server-compact-edition-connection-manager-editor-all-page"></a>SQL Server Compact Edition 연결 관리자 편집기(모든 페이지)
  **SQL Server Compact Edition 연결 관리자** 대화 상자를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 데이터베이스에 연결하기 위한 속성을 지정할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact Edition 연결 관리자에 대한 자세한 내용은 [SQL Server Compact Edition 연결 관리자](connection-manager/sql-server-compact-edition-connection-manager.md)를 참조하세요.  
  
## <a name="options"></a>옵션  
 **자동 축소 임계값**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 데이터베이스에서 자동 축소 프로세스를 실행하기 전에 허용되는 사용 가능한 공간(%)을 지정합니다.  
  
 **기본 잠금 에스컬레이션**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 데이터베이스가 잠금 에스컬레이션 전에 획득하는 데이터베이스 잠금 수를 지정합니다.  
  
 **기본 잠금 제한 시간**  
 트랜잭션에서 잠금을 대기할 기본 간격(밀리초)을 지정합니다.  
  
 **플러시 간격**  
 커밋된 트랜잭션을 디스크에 플러시하는 간격(초)을 지정합니다.  
  
 **로캘 ID**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 데이터베이스의 LCID(로캘 ID)를 지정합니다.  
  
 **최대 버퍼 크기**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact에서 데이터를 디스크에 플러시하기 전에 사용하는 최대 메모리 용량(KB)을 지정합니다.  
  
 **최대 데이터베이스 크기**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 데이터베이스의 최대 크기(MB)를 지정합니다.  
  
 **모드**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 데이터베이스를 열 파일 모드를 지정합니다. 이 속성의 기본값은 **읽기/쓰기**입니다.  
  
 다음 표에서는 모드 옵션의 4가지 값에 대해 설명합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**Read Only**|데이터베이스에 대한 읽기 전용 액세스 권한을 지정합니다.|  
|**읽기 쓰기**|데이터베이스에 대한 읽기/쓰기 권한을 지정합니다.|  
|**단독**|데이터베이스에 대한 단독 액세스 권한을 지정합니다.|  
|**공유 읽기**|다른 사용자가 데이터베이스를 동시에 읽을 수 있도록 지정합니다.|  
  
 **Persist Security Info**  
 보안 정보를 연결 문자열의 일부로 반환할지 여부를 지정합니다. 이 옵션의 기본값은 **False**입니다.  
  
 **임시 파일 디렉터리**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 임시 데이터베이스 파일의 위치를 지정합니다.  
  
 **데이터 원본**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 데이터베이스의 이름을 지정합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 데이터베이스의 암호를 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [SQL Server Compact Edition 연결 관리자 편집기&#40;연결 페이지&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
  
