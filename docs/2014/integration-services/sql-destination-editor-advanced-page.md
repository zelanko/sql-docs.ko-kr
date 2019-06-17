---
title: SQL 대상 편집기 (고급 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlserverdestadapter.advanced.f1
helpviewer_keywords:
- SQL Server Destination Editor
ms.assetid: 9b46bcf8-ddaf-4d7d-90a6-80bc19517e9b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 087f32510b65d7ea505bc4bf816a5ca9edcfe82d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055459"
---
# <a name="sql-destination-editor-advanced-page"></a>SQL 대상 편집기(고급 페이지)
  **SQL 대상 편집기** 대화 상자의 **고급** 페이지를 사용하여 고급 대량 삽입 옵션을 지정할 수 있습니다.  
  
 SQL Server 대상에 대한 자세한 내용은 [SQL Server Destination](data-flow/sql-server-destination.md)을 참조하십시오.  
  
## <a name="options"></a>변수  
 **ID 유지**  
 태스크에서 ID 열에 값을 삽입할지 여부를 지정합니다. 이 속성의 기본값은 `False`입니다.  
  
 **Null 유지**  
 태스크에서 Null 값을 유지할지 여부를 지정합니다. 이 속성의 기본값은 `False`입니다.  
  
 **테이블 잠금**  
 데이터를 로드할 때 테이블을 잠글지 여부를 지정합니다. 이 속성의 기본값은 `True`입니다.  
  
 **CHECK 제약 조건**  
 태스크에서 제약 조건을 확인할지 여부를 지정합니다. 이 속성의 기본값은 `True`입니다.  
  
 **트리거 실행**  
 대량 삽입에서 테이블에 대해 트리거를 실행할지 여부를 지정합니다. 이 속성의 기본값은 `False`입니다.  
  
 **첫 번째 행**  
 삽입할 첫 번째 행을 지정합니다. 이 속성의 기본값은 **-1**이며 이 경우 값이 할당되지 않습니다.  
  
> [!NOTE]  
>  이 속성에 값을 할당하지 않으려면 **SQL 대상 편집기** 에서 해당 입력란의 내용을 지웁니다. **속성** 창, **고급 편집기**및 개체 모델에 -1을 사용합니다.  
  
 **마지막 행**  
 삽입할 마지막 행을 지정합니다. 이 속성의 기본값은 **-1**이며 이 경우 값이 할당되지 않습니다.  
  
> [!NOTE]  
>  이 속성에 값을 할당하지 않으려면 **SQL 대상 편집기** 에서 해당 입력란의 내용을 지웁니다. **속성** 창, **고급 편집기**및 개체 모델에 -1을 사용합니다.  
  
 **최대 오류 개수**  
 대량 삽입이 중지되기 전에 발생할 수 있는 오류 수를 지정합니다. 이 속성의 기본값은 **-1**이며 이 경우 값이 할당되지 않습니다.  
  
> [!NOTE]  
>  이 속성에 값을 할당하지 않으려면 **SQL 대상 편집기** 에서 해당 입력란의 내용을 지웁니다. **속성** 창, **고급 편집기**및 개체 모델에 -1을 사용합니다.  
  
 **Timeout**  
 시간이 초과되어 대량 삽입이 중지되기까지 기다리는 시간(초)을 지정합니다.  
  
 **열 순서 지정**  
 정렬 열의 이름을 입력합니다. 각 열을 오름차순이나 내림차순으로 정렬할 수 있습니다. 여러 정렬 열을 사용하는 경우 쉼표로 목록을 구분합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [SQL 대상 편집기&#40;연결 관리자 페이지&#41;](../../2014/integration-services/sql-destination-editor-connection-manager-page.md)   
 [SQL 대상 편집기&#40;매핑 페이지&#41;](../../2014/integration-services/sql-destination-editor-mappings-page.md)   
 [SQL Server 대상을 사용하여 데이터 대량 로드](data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  
