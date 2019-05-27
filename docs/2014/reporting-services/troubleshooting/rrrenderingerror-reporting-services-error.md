---
title: rrRenderingError - Reporting Services 오류 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rrRenderingError
ms.assetid: 0751efc3-b81b-44ee-8aac-8560f86ca322
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 390cd2efde37d5d04b7b7ef3a3799222e024b7e4
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099277"
---
# <a name="rrrenderingerror---reporting-services-error"></a>rrRenderingError - Reporting Services 오류
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|rrRenderingError|  
|이벤트 원본|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources.Strings|  
|구성 요소|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|메시지 텍스트|보고서를 렌더링하는 동안 오류가 발생했습니다. (rrRenderingError) %1|  
  
## <a name="explanation"></a>설명  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 보고서를 렌더링할 수 없거나 내보낼 수 없을 때 이 메시지가 반환됩니다.  
  
 크기가 지원되지 않음을 나타내는 메시지는 지정된 RDL 페이지 크기가 유효하지 않을 때 일반적으로 발생합니다. 유효한 RDL 페이지 크기를 지정한 다음 다시 시도하세요.  
  
 RDL 크기 단위가 지원되지 않음을 나타내는 메시지는 지원되지 않는 단위 유형이 지정되었을 때 일반적으로 발생합니다. 유효한 단위 유형은 cm, in, mm, pc 및 pt입니다. 유효한 단위 유형을 지정한 다음 다시 시도하세요.  
  
 음수 크기가 지원되지 않음을 나타내는 메시지는 페이지 크기의 음수 단위(예: -5cm)가 지정되었을 때 일반적으로 발생합니다. 페이지 크기에 대해 양수를 지정한 다음 다시 시도하세요.  
  
 범위를 벗어난 RDL 크기가 지정되었음을 나타내는 메시지는 페이지 크기 단위가 유효한 페이지 여백 크기 범위를 벗어났을 때 일반적으로 발생합니다. 유효한 페이지 여백 크기 내에 있는 페이지 크기 단위를 지정하세요.  
  
 지정된 색이 지원되지 않음을 나타내는 메시지는 RDL에 지정된 색이 유효하지 않을 때 일반적으로 발생합니다. RDL에서 지원하는 색을 변경한 다음 다시 시도하세요.  
  
 단일 동작을 사용하는 경우에만 동작 레이블이 선택 사항이고 여러 동작을 추가하려면 각 동작마다 레이블이 필요함을 나타내는 메시지는 유효하지 않은 동작 레이블이 지정되었을 때 일반적으로 발생합니다. 각 동작마다 유효한 동작 레이블을 지정하세요.  
  
 스타일 인수가 특정 유형이어야 함을 나타내는 메시지는 데이터 형식에 대해 잘못된 스타일 값이 지정되었을 때 일반적으로 발생합니다. RDL 사양은 다른 RDL 요소의 스타일 값에서 사용할 수 있는 유효한 유형을 식별합니다. 예를 들어 배경색에 대해 잘못된 스타일 값은 "2pt"이고 높이에 대해 잘못된 값은 "true"입니다. 올바른 값을 지정한 다음 다시 시도하세요.  
  
 테두리 스타일이 지원되지 않음을 나타내는 메시지는 지정된 테두리 스타일이 유효하지 않을 때 일반적으로 발생합니다. 지원되는 테두리 스타일을 지정한 다음 다시 시도하세요.  
  
 이미지 MIME 형식이 지원되지 않음을 나타내는 메시지는 이미지 보고서 항목에 대해 지정된 MIME 형식이 유효하지 않을 때 일반적으로 발생합니다. 보고서 항목에 대해 지원되는 MIME 형식을 지정한 다음 다시 시도하세요.  
  
 행 개수가 시트에서 허용되는 최대 행 개수를 초과했음을 나타내는 메시지는 Excel 워크시트의 행 개수를 초과했을 때 일반적으로 발생합니다. Excel에서는 최대 65,000개의 행을 지원합니다.  
  
 열 개수가 시트에서 허용되는 최대 열 개수를 초과했음을 나타내는 메시지는 Excel 워크시트의 열 개수를 초과했을 때 일반적으로 발생합니다.  
  
## <a name="user-action"></a>사용자 동작  
  
## <a name="internal-only"></a>내부 전용  
  
