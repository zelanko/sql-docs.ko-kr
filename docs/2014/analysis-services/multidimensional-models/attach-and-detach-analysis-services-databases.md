---
title: Analysis Services 데이터베이스 연결 및 분리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssms.detachdatabase.f1
- sql12.asvs.ssms.attachdatabase.f1
- sql12.asvs.ssmsimbi.AttachDatabase.f1
- sql12.asvs.ssmsimbi.DetachDatabase.f1
helpviewer_keywords:
- databases [Analysis Services], attach
- databases [Analysis Services], detach
ms.assetid: 41887413-2d47-49b8-8614-553cb799fb18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4447f58baaa5ea88a48c67a9a32fcda77681d8d4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077492"
---
# <a name="attach-and-detach-analysis-services-databases"></a>Analysis Services 데이터베이스 연결 및 분리
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DBA(데이터베이스 관리자)는 종종 일정 기간 동안 데이터베이스를 오프라인 상태로 유지하다가 동일한 서버 인스턴스 또는 다른 서버 인스턴스에서 해당 데이터베이스를 다시 온라인 상태로 되돌려야 하는 경우가 있습니다. 이러한 경우는 보다 나은 성능, 데이터베이스 확장에 따른 공간 확보, 또는 제품 업그레이드를 위해 데이터베이스를 다른 디스크로 이동하는 것과 같이 대부분 비즈니스 요구 사항에 의해 발생합니다. 이러한 모든 상황은 물론 다른 상황에서도 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DBA는 `Attach` 및 `Detach` 명령을 사용하여 아주 간단히 데이터베이스를 오프라인 상태로 유지하다가 다시 온라인 상태로 만들 수 있습니다.  
  
## <a name="attach-and-detach-commands"></a>Attach 및 Detach 명령  
 `Attach` 명령을 사용하면 오프라인 상태였던 데이터베이스를 온라인 상태로 만들 수 있습니다. 데이터베이스를 원래 서버 인스턴스나 다른 인스턴스에 연결할 수 있습니다. 데이터베이스를 연결하면 사용자가 데이터베이스에 대해 **ReadWriteMode** 설정을 지정할 수 있습니다. `Detach` 명령을 사용하면 데이터베이스를 서버로부터 오프라인 상태로 만들 수 있습니다.  
  
## <a name="attach-and-detach-usage"></a>Attach 및 Detach 용도  
 `Attach` 명령은 기존 데이터베이스 구조를 온라인 상태로 만드는 데 사용됩니다. 데이터베이스가 `ReadWrite` 모드로 연결된 경우 서버 인스턴스에 한 번만 연결할 수 있지만 `ReadOnly` 모드로 연결된 경우에는 여러 서버 인스턴스에 여러 번 연결할 수 있습니다. 하지만 동일한 데이터베이스를 동일한 서버 인스턴스에 두 번 이상 연결할 수는 없습니다. 동일한 데이터베이스를 두 번 이상 연결하려고 하면 데이터가 별개의 폴더에 복사되었더라도 오류가 발생합니다.  
  
> [!IMPORTANT]  
>  데이터 분리 시 암호가 필요했다면 데이터베이스 연결 시에도 동일한 암호가 필요합니다.  
  
 `Detach` 명령은 기존 데이터베이스 구조를 오프라인 상태로 만드는 데 사용됩니다. 데이터베이스를 분리할 때는 기밀 메타데이터 보호를 위해 암호를 제공해야 합니다.  
  
> [!IMPORTANT]  
>  데이터 파일의 내용을 보호하려면 폴더, 하위 폴더 및 데이터 파일에 대한 액세스 제어 목록을 사용해야 합니다.  
  
 데이터베이스 분리 시 서버는 다음 단계를 수행합니다.  
  
|읽기/쓰기 데이터베이스 분리|읽기 전용 데이터베이스 분리|  
|--------------------------------------|-------------------------------------|  
|1) 서버가 데이터베이스에 대한 CommitExclusive 잠금 요청을 실행합니다.<br />2) 서버가 진행 중인 모든 트랜잭션이 커밋되거나 롤백될 때까지 기다립니다.<br />3) 서버가 데이터베이스 분리를 위해 필요한 모든 메타데이터를 작성합니다.<br />4) 데이터베이스가 삭제된 것으로 표시됩니다.<br />5) 서버가 트랜잭션을 커밋합니다.|1) 데이터베이스가 삭제된 것으로 표시됩니다.<br />2) 서버가 트랜잭션을 커밋합니다.<br /><br /> <br /><br /> 참고: 읽기 전용 데이터베이스에 대 한 분리 암호는 변경할 수 없습니다. 암호를 이미 포함하고 있는 연결된 데이터베이스에 암호 매개 변수를 제공하면 오류가 발생합니다.|  
  
 `Attach` 및 `Detach` 명령은 단일 작업으로 실행해야 하며 동일 트랜잭션 내 다른 작업과 결합할 수 없습니다. 또한 합니다 `Attach` 및 `Detach` 명령은 원자성 트랜잭션 명령 됩니다. 작업이 성공하거나 실패하거나 둘 중 하나입니다. 완료되지 않은 상태로 남는 데이터베이스는 없습니다.  
  
> [!IMPORTANT]  
>  `Detach` 명령을 실행하려면 서버 또는 데이터베이스 관리자 권한이 필요합니다.  
  
> [!IMPORTANT]  
>  `Attach` 명령을 실행하려면 서버 관리자 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Analysis Services 데이터베이스 이동](move-an-analysis-services-database.md)   
 [ReadWriteMode 데이터베이스](database-readwritemodes.md)   
 [ReadOnly 모드와 ReadWrite 모드 간 Analysis Services 데이터베이스 전환](switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)   
 [Detach 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [Attach 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)  
  
  
