---
title: 플랫 파일 대상 편집기 (연결 관리자 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfiledestadapter.connection.f1
helpviewer_keywords:
- Flat File Destination Editor
ms.assetid: b01571fa-bc19-4742-8eed-ac163172a919
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 429ba1f8a12a4bd574a8304d18311a6e6e4efc79
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058701"
---
# <a name="flat-file-destination-editor-connection-manager-page"></a>플랫 파일 대상 편집기(연결 관리자 페이지)
  **플랫 파일 대상 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 대상에 사용할 플랫 파일 연결을 선택하고, 덮어쓸 것인지 아니면 기존 대상 파일에 추가할 것인지를 지정할 수 있습니다. 플랫 파일 대상에서는 텍스트 파일에 데이터를 기록합니다. 이 텍스트 파일은 구분 기호로 분리하거나 고정 폭, 구분 기호 있는 고정 폭 또는 왼쪽 정렬 중 하나를 사용할 수 있습니다.  
  
 플랫 파일 대상에 대한 자세한 내용은 [Flat File Destination](data-flow/flat-file-destination.md)을 참조하십시오.  
  
## <a name="options"></a>변수  
 **플랫 파일 연결 관리자**  
 목록 상자를 사용하여 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **플랫 파일 형식** 대화 상자와 **플랫 파일 연결 관리자 편집기** 대화 상자를 사용하여 새 연결을 만듭니다.  
  
 **플랫 파일 형식** 대화 상자에는 표준 플랫 파일 형식인 구분 기호로 분리됨, 고정 폭 및 왼쪽 정렬 이외에도 **고정 폭, 행 구분 기호 사용**옵션이 표시됩니다. 이 옵션은 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 더미 열을 데이터의 마지막 열로 추가할 때 사용하는 왼쪽 정렬 형식의 특별한 경우를 나타냅니다. 이 더미 열은 마지막 열이 고정 폭을 갖도록 합니다.  
  
 **고정 폭, 행 구분 기호 사용** 옵션은 **플랫 파일 연결 관리자 편집기**에서 사용할 수 없습니다. 필요한 경우 편집기에서 이 옵션을 에뮬레이트할 수는 있습니다. 이 옵션을 에뮬레이트하려면 **플랫 파일 연결 관리자 편집기** 대화 상자의 **일반**페이지에서 **형식**으로 **왼쪽 정렬**을 선택합니다. 그런 다음 편집기의 **고급** 페이지에서 새 더미 열을 데이터의 마지막 열로 추가합니다.  
  
 **파일의 데이터 덮어쓰기**  
 기존 파일을 덮어쓸지 아니면 기존 파일에 데이터를 추가할지 여부를 나타냅니다.  
  
 **머리글**  
 데이터를 쓰기 전에 삽입할 텍스트 블록을 입력합니다. 이 옵션을 사용하여 열 머리글 등의 추가 정보를 포함할 수 있습니다.  
  
 **미리 보기**  
 **데이터 보기** 대화 상자를 사용하여 결과를 미리 봅니다. 미리 보기에는 최대 200개의 행이 표시될 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [플랫 파일 대상 편집기&#40;매핑 페이지&#41;](../../2014/integration-services/flat-file-destination-editor-mappings-page.md)  
  
  
