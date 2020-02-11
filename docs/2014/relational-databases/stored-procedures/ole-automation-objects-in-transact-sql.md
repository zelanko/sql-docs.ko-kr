---
title: Transact-SQL의 OLE 자동화 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], OLE Automation
- batches [SQL Server], OLE Automation
- OLE Automation [SQL Server]
- OLE Automation [SQL Server], about OLE Automation
ms.assetid: a887d956-4cd0-400a-aa96-00d7abd7c44b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 06913c27af89657aef5a0a5397cd77a1ee025299
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211850"
---
# <a name="ole-automation-objects-in-transact-sql"></a>Transact-SQL의 OLE 자동화 개체
  [!INCLUDE[tsql](../../includes/tsql-md.md)]에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리, 저장 프로시저 및 트리거에서 OLE 자동화 개체를 참조할 수 있도록 하는 몇 가지 시스템 저장 프로시저가 포함 되어 있습니다. 이러한 시스템 저장 프로시저는 확장 저장 프로시저처럼 실행되며 저장 프로시저를 통해 실행되는 OLE Automation 개체는 확장 저장 프로시저와 같은 방식으로 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스의 주소 공간에서 실행됩니다.  
  
 OLE Automation 저장 프로시저를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리에서 **IDispatch** 인터페이스를 제공하는 개체와 같은 사용자 지정 OLE Automation 개체와 SQL-DMO 개체를 참조할 수 있습니다. 
  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 를 사용하여 만들어진 사용자 지정 종속 프로세스 OLE 서버에는 **On Error GoTo** 및 **On Error GoTo** 서브루틴에 대한 오류 처리기( **On Error GoTo** 문으로 지정)가 있어야 합니다. 
  **Class_Initialize** 및 **Class_Terminate** 서브루틴의 오류가 처리되지 않을 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스의 액세스 위반과 같은 예상치 못한 오류가 발생할 수 있습니다. 또한 다른 서브루틴에 대한 오류 처리기도 권장됩니다.  
  
 
  [!INCLUDE[tsql](../../includes/tsql-md.md)]의 OLE Automation 개체를 사용하려면 우선 **sp_OACreate** 시스템 저장 프로시저를 호출하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스의 주소 공간에 개체의 인스턴스를 만들어야 합니다.  
  
 개체의 인스턴스가 생성된 후에는 다음과 같은 저장 프로시저를 호출하여 개체의 속성, 메서드 및 개체 관련 오류 정보에 대한 작업을 수행합니다.  
  
-   **sp_OAGetProperty** 은 속성의 값을 가져옵니다.  
  
-   **sp_OASetProperty** 은 속성의 값을 설정 합니다.  
  
-   **sp_OAMethod** 는 메서드를 호출 합니다.  
  
-   최신 오류 정보를 얻을 **sp_OAGetErrorInfo** .  
  
 개체가 더 이상 필요하지 않을 때는 **sp_OADestroy** 를 호출하여 **sp_OACreate**로 생성된 개체의 인스턴스를 할당 취소합니다.  
  
 OLE Automation 개체는 속성 값과 메서드를 통해 데이터를 반환합니다. **sp_OAGetProperty** 및 **sp_OAMethod** 는 결과 집합의 형식으로 이러한 데이터 값을 반환 합니다.  
  
 OLE Automation 개체의 범위는 일괄 처리입니다. 개체의 모든 참조는 하나의 일괄 처리, 저장 프로시저 또는 트리거 안에 들어 있어야 합니다.  
  
 개체를 참조할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE 자동화 개체는 참조되는 개체 안에 포함된 다른 개체들 간의 순회 검색을 지원합니다. 예를 들어 SQL-DMO **SQLServer** 개체를 사용할 때 해당 서버에 포함된 데이터베이스와 테이블에 대한 참조를 만들 수 있습니다.  
  
## <a name="related-content"></a>관련 내용  
 [Transact-sql&#41;&#40;개체 계층 구조 구문](/sql/relational-databases/system-stored-procedures/object-hierarchy-syntax-transact-sql)  
  
 [노출 영역 구성](../security/surface-area-configuration.md)  
  
 [Ole Automation Procedures 서버 구성 옵션](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)  
  
 [sp_OACreate&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oacreate-transact-sql)  
  
 [sp_OAGetProperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oagetproperty-transact-sql)  
  
 [sp_OASetProperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oasetproperty-transact-sql)  
  
 [sp_OAMethod&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oamethod-transact-sql)  
  
 [sp_OAGetErrorInfo&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oageterrorinfo-transact-sql)  
  
 [sp_OADestroy&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oadestroy-transact-sql)  
  
  
