---
title: 유사 항목 조회 변환 편집기 (참조 테이블 탭) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptransformation.referencetable.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: 451f4e7d-1c8e-4784-b540-df0806509bf1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: eb86e4a6382095bb8bb0edc744fe6d16650581fd
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425210"
---
# <a name="fuzzy-lookup-transformation-editor-reference-table-tab"></a>유사 항목 조회 변환 편집기(참조 테이블 탭)
  **유사 항목 조회 변환 편집기** 대화 상자의 **참조 테이블** 탭을 사용하여 조회 시 사용할 원본 테이블 및 인덱스를 지정할 수 있습니다. 참조 데이터 원본은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 있는 테이블이어야 합니다.  
  
> [!NOTE]  
>  유사 항목 조회 변환은 참조 테이블의 작업 복사본을 만듭니다. 아래에서 설명하는 인덱스는 일반 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인덱스가 아닌 특수 테이블을 사용하여 이 작업 테이블에 생성됩니다. **저장된 인덱스 유지 관리**를 선택하지 않으면 변환에서 기존 원본 테이블을 수정하지 않습니다. 이 경우 변환에서는 참조 테이블에 대한 변경 내용을 기반으로 작업 테이블 및 조회 인덱스 테이블을 업데이트하는 트리거를 참조 테이블에 만듭니다.  
  
> [!NOTE]  
>  유사 `Exhaustive` `MaxMemoryUsage` 항목 조회 변환의 및 속성은 **유사 항목 조회 변환 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용 하 여 설정할 수 있습니다. 또한에 대 한 100 보다 큰 값은 `MaxOutputMatchesPerInput` **고급 편집기**에서만 지정할 수 있습니다. 이러한 속성에 대한 자세한 내용은 [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md)의 유사 항목 조회 변환 섹션을 참조하십시오.  
  
 유사 항목 조회 변환에 대한 자세한 내용은 [Fuzzy Lookup Transformation](data-flow/transformations/lookup-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **OLE DB 연결 관리자**  
 목록에서 기존 OLE DB 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새 항목**  
 **OLE DB 연결 관리자 구성** 대화 상자를 사용하여 새 연결을 만듭니다.  
  
 **새 인덱스 생성**  
 변환에서 조회 시 사용할 새 인덱스를 만들도록 지정합니다.  
  
 **참조 테이블 이름**  
 참조(조회) 테이블로 사용할 기존 테이블을 선택합니다.  
  
 **새 인덱스 저장**  
 새 조회 인덱스를 저장하려면 이 옵션을 선택합니다.  
  
 **새 인덱스 이름**  
 새 조회 인덱스를 저장하도록 선택한 경우 해당 인덱스를 설명하는 이름을 입력합니다.  
  
 **저장된 인덱스 유지 관리**  
 새 조회 인덱스를 저장하도록 선택한 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 해당 인덱스를 유지 관리하도록 할지 여부를 지정합니다.  
  
> [!NOTE]  
>  **유사 항목 조회 변환 편집기** 의 **참조 테이블** 에서 **저장된 인덱스 유지 관리**를 선택하면 변환은 관리 저장 프로시저를 사용하여 인덱스를 유지 관리합니다. 이러한 관리 저장 프로시저는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 CLR(공용 언어 런타임) 통합 기능을 사용합니다. 기본적으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 CLR 통합은 사용되지 않습니다. **저장된 인덱스 유지 관리** 기능을 사용하려면 CLR 통합을 사용하도록 설정해야 합니다. 자세한 내용은 [Enabling CLR Integration](../relational-databases/clr-integration/clr-integration-enabling.md)을 참조하세요.  
>   
>  **저장된 인덱스 유지 관리** 옵션에는 CLR 통합이 필요하므로 CLR 통합이 사용되는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 인스턴스에 있는 참조 테이블을 선택하는 경우에만 이 기능이 작동합니다.  
  
 **기존 인덱스 사용**  
 변환에서 조회 시 기존 인덱스를 사용하도록 지정합니다.  
  
 **기존 인덱스의 이름**  
 목록에서 이전에 만든 조회 인덱스를 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [유사 항목 조회 변환 편집기 &#40;열 탭&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-columns-tab.md)   
 [유사 항목 조회 변환 편집기&#40;고급 탭&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  
