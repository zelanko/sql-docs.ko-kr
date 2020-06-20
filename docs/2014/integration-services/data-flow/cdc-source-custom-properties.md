---
title: CDC 원본 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 744e9357-94a9-4202-abe8-1d3d202697e9
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ebb2869899ab670a55ba2fcdafdfb1276f9207fa
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84916625"
---
# <a name="cdc-source-custom-properties"></a>CDC 원본 사용자 지정 속성
  다음 표에서는 CDC 원본의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|연결|ADO.Net 연결|변경 테이블에 액세스하기 위한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC 데이터베이스에 대한 ADO.NET 연결입니다.|  
|StateVariable|String|현재 CDC 실행의 CDC 상태를 유지 관리하는 SSIS 문자열 패키지 변수입니다.|  
|CdcProcessingMode|Integer(열거형)|이 모드는 처리 진행 방법을 결정합니다. 가능한 옵션은 **모두**, **이전 값이 포함된 모두**, **순**, **업데이트 마스크를 사용한 순 변경 내용**및 **병합을 사용한 순 변경 내용**입니다.<br /><br /> 모두가 포함된 모드는 모든 변경 내용을 반환하고 순이 포함된 모드는 순 변경 내용만 반환합니다.<br /><br /> 기본 키가 없는 테이블에는 모두 값만 사용할 수 있습니다.<br /><br /> **업데이트 마스크가 있는 Net** 은 이름 패턴 **__ $ \<column-name> \_ _Changed** 인 부울 열을 추가 하 여 현재 변경 행에서 변경 된 열을 표시 합니다.<br /><br /> 이 속성의 값에 대한 자세한 내용은 [CDC 원본 편집기&#40;연결 관리자 페이지&#41;](../cdc-source-editor-connection-manager-page.md)를 참조하세요.|  
|CaptureInstance|String|읽을 CDC 테이블이 포함된 CDC 캡처 인스턴스의 이름입니다. 캡처된 원본 테이블에는 스키마 변경을 통해 테이블 정의의 원활한 전환을 처리하도록 하나 또는 두 개의 캡처된 인스턴스가 포함되어 있을 수 있습니다. 캡처할 원본 테이블에 대해 두 개 이상의 캡처 인스턴스가 정의되어 있으면 여기에서 사용할 캡처 인스턴스를 선택합니다. 테이블 [schema]의 기본 캡처 인스턴스 이름입니다. [table]은 \<schema> _ \<table> 이지만 실제로 사용 중인 캡처 인스턴스 이름은 다를 수 있습니다. 에서 읽는 실제 테이블은 CDC 테이블 **cdc입니다. \<capture-instance> _CT**.|  
|ReprocessingIndicator|부울|**__$reprocessing** 열을 추가할지 여부를 지정하는 값입니다. 이 특수 출력 열을 사용하면 초기 처리 범위에서 작업할 때 SSIS 개발자가 일관성 오류를 다르게 처리할 수 있습니다.<br /><br /> **true**이면  **__$reprocessing** 열이 추가됩니다.<br /><br /> CDC 처리 범위가 초기 처리 범위(초기 로드 기간에 해당하는 LSN의 범위)와 겹치거나 이전 실행의 오류 발생 후 CDC 처리 범위가 다시 처리되는 경우 이 열 값은 **true** 입니다. 이 표시기 열을 사용하면 변경 내용을 다시 처리할 때 SSIS 개발자가 오류를 다르게 처리할 수 있습니다. 예를 들어 존재하지 않는 행의 삭제와 중복 키에 대해 실패한 삽입과 같은 동작은 무시할 수 있습니다.<br /><br /> 기본 값은 **false**입니다.|  
|CommandTimeout|정수|이 값은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 데이터베이스와 통신할 때 사용할 제한 시간(초)을 나타냅니다. 이 값은 데이터베이스로부터의 응답이 매우 느리고 기본값(30초)이 충분하지 않은 경우 사용됩니다.|  
  
 CDC 원본에 대한 자세한 내용은 [CDC Source](cdc-source.md)을 참조하십시오.  
  
  
