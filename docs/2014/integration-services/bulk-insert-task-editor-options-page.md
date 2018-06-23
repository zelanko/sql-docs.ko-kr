---
title: 대량 삽입 태스크 편집기 (옵션 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.bulkinserttask.options.f1
helpviewer_keywords:
- Bulk Insert Task Editor
ms.assetid: b3702811-3eb8-4b28-9190-5ae7a1a7bb6f
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a1a958108c8b6975c3aa362ba6512b995759ff99
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187677"
---
# <a name="bulk-insert-task-editor-options-page"></a>대량 삽입 태스크 편집기(옵션 페이지)
  **대량 삽입 태스크 편집기** 대화 상자의 **옵션** 페이지를 사용하여 대량 삽입 작업에 대한 옵션을 설정할 수 있습니다. 대량 삽입 태스크는 대량의 데이터를 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 테이블 또는 뷰로 복사합니다.  
  
 대량 삽입 작업에 대한 자세한 내용은 [대량 삽입 태스크](control-flow/bulk-insert-task.md) 및 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)를 참조하세요.  
  
## <a name="options"></a>변수  
 **CodePage**  
 데이터 파일에서 데이터의 코드 페이지를 지정합니다.  
  
 **DataFileType**  
 로드 작업에 사용할 데이터 형식 값을 지정합니다.  
  
 **BatchSize**  
 일괄 처리의 행 수를 지정합니다. 전체 데이터 파일이 기본값입니다. **BatchSize** 를 0으로 설정하면 데이터가 단일 일괄 처리로 로드됩니다.  
  
 **LastRow**  
 복사할 마지막 행을 지정합니다.  
  
 **FirstRow**  
 복사를 시작할 처음 행을 지정합니다.  
  
 **대량 삽입 태스크 편집기**  
 |용어|정의|  
|----------|----------------|  
|**CHECK 제약 조건**|테이블 및 열 제약 조건을 확인하려면 선택합니다.|  
|**Null 유지**|대량 삽입 작업 중에 빈 열에 기본값을 삽입하는 대신 Null 값을 유지하려면 선택합니다.|  
|**ID 삽입 가능**|기존 값을 ID 열에 삽입하려면 선택합니다.|  
|**테이블 잠금**|대량 삽입 중에 테이블을 잠그려면 선택합니다.|  
|**트리거 실행**|테이블에 삽입, 업데이트 또는 삭제 트리거를 발생시키려면 선택합니다.|  
  
 **SortedData**  
 대량 삽입 문에 ORDER BY 절을 지정합니다. 사용자가 제공한 열 이름은 대상 테이블에서 유효한 열이어야 합니다. 기본값은 `false`입니다. 즉, 데이터는 ORDER BY 절로 정렬되지 않습니다.  
  
 **MaxErrors**  
 대량 삽입 작업이 취소되는 최대 오류 발생 횟수를 지정합니다. 값을 0으로 지정하면 오류가 무한으로 발생해도 작업이 취소되지 않습니다.  
  
> [!NOTE]  
>  대량 로드 작업으로 가져올 수 없는 각 행은 하나의 오류로 간주됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [대량 삽입 태스크 편집기 &#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [대량 삽입 태스크 편집기 &#40;연결 페이지&#41;](../../2014/integration-services/bulk-insert-task-editor-connection-page.md)   
 [식 페이지](expressions/expressions-page.md)   
 [제어 흐름](control-flow/control-flow.md)  
  
  
