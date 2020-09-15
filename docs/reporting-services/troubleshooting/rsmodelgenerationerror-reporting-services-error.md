---
title: rsModelGenerationError - Reporting Services 오류 | Microsoft Docs
description: 이 오류 참조 페이지에서 이벤트 ID 107 'rsModelGenerationError'에 대해 알아봅니다. 모델을 생성하는 동안 오류가 발생했습니다.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rsModelGenerationError
ms.assetid: 3a0ad63f-87f9-4ca1-b0c2-c85fa991634a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d49619a5005b542478f5be971b5206f492b66027
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396743"
---
# <a name="rsmodelgenerationerror---reporting-services-error"></a>rsModelGenerationError - Reporting Services 오류
    
## <a name="details"></a>세부 정보  
  
|범주|값|  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|rsRenderingError|  
|이벤트 원본|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|구성 요소|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|메시지 텍스트|모델을 생성하는 동안 오류가 발생했습니다. (rsModelGenerationError) (ReportingServicesLibrary) %1|  
  
## <a name="explanation"></a>설명  
 보고서 모델을 생성할 수 없습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 SP1 및 이전 버전에서 이 오류는 예를 들어 두 개의 외래 키가 한 테이블 내에서 같은 열에 정의된 경우처럼 System.Data.DataSet 개체가 데이터베이스 스키마 내에서 테이블이나 관계를 처리할 수 없을 경우 주로 표시됩니다.  
  
## <a name="user-action"></a>사용자 동작  
 이러한 메시지를 표시하는 특정 원인을 확인하려면 \Microsoft SQL Server\\<SQL Server Instance\>\Reporting Services\LogFiles에 있는 보고서 서버 로그 파일을 검토하세요.  
  
## <a name="internal-only"></a>내부 전용  
  
