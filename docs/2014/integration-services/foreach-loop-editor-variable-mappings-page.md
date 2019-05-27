---
title: Foreach 루프 편집기 (변수 매핑 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.mapping.f1
ms.assetid: aa847b87-f391-48a5-9849-eeda2d6b00b9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03488e4cfd3a0cc905a58166f381f68eb3292c49
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058533"
---
# <a name="foreach-loop-editor-variable-mappings-page"></a>Foreach 루프 편집기(변수 매핑 페이지)
  **Foreach 루프 편집기** 대화 상자의 **변수 매핑** 페이지를 사용하여 변수를 컬렉션 값에 매핑할 수 있습니다. 변수 값은 루프가 반복될 때마다 컬렉션 값으로 업데이트됩니다.  
  
 Integration Services 패키지의 Foreach 루프 컨테이너를 사용하는 방법은 [Foreach Loop Container](control-flow/foreach-loop-container.md) 를 참조하십시오. 구성 방법에 대한 자세한 내용은 [Foreach 루프 컨테이너 구성](../../2014/integration-services/configure-a-foreach-loop-container.md)을 참조하세요.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 자습서인 간단한 ETL 패키지 만들기 자습서에는 Foreach 루프를 추가 및 구성하는 방법을 배울 수 있는 단원이 있습니다.  
  
## <a name="options"></a>Options  
 **변수**  
 기존 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
> [!NOTE]  
>  변수를 매핑하면 새 행이 **변수** 목록에 자동으로 추가됩니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
 **Index**  
 Foreach Item 열거자를 사용하는 경우 컬렉션 값에서 변수에 매핑할 열의 인덱스를 지정합니다. 다른 유형의 열거자를 사용하는 경우 인덱스는 읽기 전용입니다.  
  
> [!NOTE]  
>  인덱스는 0부터 시작합니다.  
  
 **관련 항목**: [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
 **Delete**  
 변수를 선택한 다음 **삭제**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Foreach 루프 편집기 &#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [Foreach 루프 편집기 &#40;컬렉션 페이지&#41;](../../2014/integration-services/foreach-loop-editor-collection-page.md)   
 [식 페이지](expressions/expressions-page.md)   
 [For 루프 컨테이너](control-flow/for-loop-container.md)  
  
  
