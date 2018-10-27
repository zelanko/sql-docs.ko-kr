---
title: 연결 속성 대화 상자 (SSAS-테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.ConnectionProperties.F1
ms.assetid: 17bae8ae-2ba0-4978-be70-61c687f59d54
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3322b71162b93204591dbb1c0bffb6bac4856454
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148398"
---
# <a name="connection-properties-dialog-box-ssas---tabular"></a>연결 속성 대화 상자(SSAS - 테이블 형식)
  이 페이지를 사용하여 SQL Server Management Studio에서 테이블 형식 모델 데이터베이스에 사용되는 데이터 원본의 연결 속성을 보거나 수정할 수 있습니다.  
  
 이 대화 상자에서는 타임스탬프, 기타 설명 정보 및 연결 특성을 결정하는 사용자 지정 가능 속성을 제공합니다.  
  
## <a name="options"></a>변수  
  
|용어|정의|  
|----------|----------------|  
|**이름**|데이터 원본의 이름을 지정합니다.|  
|**ID**|데이터 원본 개체의 식별자를 표시합니다.|  
|**설명**|데이터 원본 개체의 설명을 표시합니다.|  
|**생성된 타임스탬프**|데이터베이스를 만든 날짜와 시간을 표시합니다.|  
|**최종 스키마 업데이트**|데이터베이스에 대한 메타데이터를 마지막으로 업데이트한 날짜와 시간을 표시합니다.|  
|**연결 문자열**|모델에 데이터를 제공하는 데이터 원본에 연결하는 데 사용되는 연결 문자열을 표시합니다.|  
|**최대 연결 수**|이 데이터베이스에 대한 최대 클라이언트 연결 수를 지정합니다.|  
|**격리성**|유효한 값은 ReadCommitted 또는 Snapshot입니다. 자세한 내용은 [Isolation 요소&#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/isolation-element-assl)를 참조하세요.|  
|**쿼리 제한 시간**|데이터 검색 시도의 제한 시간(초)을 지정합니다.|  
|**관리 공급자**|관리 공급자의 이름을 지정합니다. 데이터 원본 연결에서 네이티브 OLE DB 공급자를 사용하는 경우에는 이 값이 비어 있습니다.|  
|**가장 정보**|데이터, 관계형 데이터 저장소에 대해 DirectQuery를 통해 실행된 쿼리, 아웃오브 라인 바인딩, 원격 파티션, 대상에서 원본으로의 데이터베이스 동기화를 처리하거나 새로 고칠 때 데이터베이스 연결에 사용되는 가장 계정을 지정합니다.<br /><br /> 유효한 값은 Analysis Services 서비스 계정 또는 특정 Windows 자격 증명 집합입니다. **현재 사용자의 자격 증명 사용** 이나 **상속**을 지정하지 마십시오. 이러한 자격 증명 옵션은 테이블 형식 모델 데이터베이스에는 지원되지 않습니다.|  
  
  
