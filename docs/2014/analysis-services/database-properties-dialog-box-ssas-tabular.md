---
title: 데이터베이스 속성 대화 상자 (SSAS-테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.DatabaseProperties.f1
ms.assetid: 0f0ec02f-7b55-40ea-8a04-ed0deb1efd7a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f8204913babd9b52caf2edcaa2de8feae76c70d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105693"
---
# <a name="database-properties-dialog-box-ssas---tabular"></a>데이터베이스 속성 대화 상자(SSAS - 테이블 형식)
  이 대화 상자에서는 타임스탬프, 기타 설명 정보 및 데이터베이스가 캐시된 데이터를 사용하는지 여부를 결정하는 사용자 지정 가능 속성을 제공합니다. 이 외에도 데이터베이스 이름 변경 및 가장 옵션 같은 사용자 지정 가능 속성이 있습니다.  
  
## <a name="options"></a>변수  
  
|용어|정의|  
|----------|----------------|  
|**이름**|**이름** 은 서버에서 데이터베이스를 고유하게 식별하는 데이터베이스 이름입니다. 데이터베이스 이름을 변경할 경우 기존 연결 문자열의 현재 이름을 사용하는 보고서와 클라이언트 애플리케이션에 어떤 영향을 주게 될지 고려하십시오. 액세스 거부 오류가 발생하지 않도록 하려면 기존 보고서의 연결 문자열을 업데이트해야 합니다. 또한 이 데이터베이스의 원본인 테이블 형식 모델에서도 원래 이름을 사용할 가능성이 높습니다. 모델의 데이터베이스 배포 속성을 업데이트하여 향후 해당 모델에 대한 업데이트가 의도한 데이터베이스에 게시되도록 하십시오.|  
|**ID**|데이터베이스의 식별자를 표시합니다.|  
|**설명**|데이터베이스에 대한 설명을 변경하려면 입력합니다.|  
|**생성된 타임스탬프**|데이터베이스를 만든 날짜와 시간을 표시합니다.|  
|**최종 스키마 업데이트**|데이터베이스에 대한 메타데이터를 마지막으로 업데이트한 날짜와 시간을 표시합니다.|  
|**마지막 업데이트**|데이터베이스에 대한 데이터를 마지막으로 업데이트한 날짜와 시간을 표시합니다.|  
|**읽기-쓰기 모드**|이 속성은 읽기 전용이지만 **분리** 명령과 **연결** 명령을 연속해서 사용하여 변경할 수 있습니다. 이 경우 이 속성은 **연결** 명령의 매개 변수입니다. 자세한 내용은 [ReadWriteMode 데이터베이스](multidimensional-models/database-readwritemodes.md)를 참조하세요.|  
|**DirectQueryMode**|데이터베이스에서 메모리 내 저장소만 사용하는지(디스크 저장소를 사용하지 않음) 디스크 기반 저장소만 사용하는지 또는 둘을 결합해서 사용하는지 여부를 지정합니다. 유효한 값은 InMemory, DirectQuery, InMemoryWithDirectQuery(대부분 메모리 기반이며 일부는 디스크로 페이징함) 또는 DirectQueryWithInMemory(대부분 디스크 기반이며 일부는 메모리 내 저장소를 사용함)입니다. 자세한 내용은 [DirectQuery 배포 시나리오 &#40;&AMP;#40;SSAS 테이블 형식&#41;](directquery-deployment-scenarios-ssas-tabular.md)합니다.|  
|**데이터 원본 가장 정보**|로컬 또는 원격 파티션의 데이터, 관계형 데이터 저장소에 대해 DirectQuery를 통해 실행된 쿼리, 아웃오브 라인 바인딩, 대상에서 원본으로의 데이터베이스 동기화를 처리하거나 새로 고칠 때 데이터베이스 연결에 사용되는 가장 계정을 지정합니다.<br /><br /> 유효한 값은 Analysis Services 서비스 계정 또는 특정 Windows 자격 증명 집합입니다. **현재 사용자의 자격 증명 사용**을 지정하지 마십시오. 이 자격 증명 옵션은 테이블 형식 모델 데이터베이스에는 지원되지 않습니다.|  
|**마지막으로 처리**|데이터베이스를 마지막으로 처리한 날짜와 시간을 표시합니다.|  
|**예상된 크기**|데이터베이스의 예상 크기를 표시합니다.|  
|**저장소 위치**|데이터베이스의 위치를 지정합니다. 데이터베이스가 기본 데이터 디렉터리에 있으면 이 값은 비어 있게 됩니다.|  
  
  
