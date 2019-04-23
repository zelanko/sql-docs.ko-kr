---
title: 보고서 서버 항목 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- report servers [Reporting Services], properties
- item-specific properties [Reporting Services]
- report items [Reporting Services], properties
- items [Reporting Services], properties
ms.assetid: 21edec6d-9897-48fb-8c75-182305b1dbdb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6ed8a56892cfd70b43341ffff8349faa56094a97
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158019"
---
# <a name="report-server-item-properties"></a>보고서 서버 항목 속성
  항목 속성은 보고서 서버 데이터베이스의 항목에 대한 특정 속성입니다. 이러한 항목에는 보고서, 링크된 보고서, 폴더, 리소스, 모델 및 데이터 원본이 포함됩니다.  
  
 다음 항목 속성 이름은 예약되어 있습니다. 동일한 이름의 사용자 정의 속성을 만들 수 없습니다. 이러한 속성 중 상당수는 보고서 서버 웹 서비스 메서드를 사용하여 읽거나 수정할 수 있습니다.  
  
## <a name="item-properties"></a>항목 속성  
 다음 속성은 보고서 서버 데이터베이스의 모든 항목에 적용됩니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**CreatedBy**|처음에 항목을 보고서 서버 데이터베이스에 추가한 사용자의 이름입니다.|  
|**CreationDate**|항목이 보고서 서버 데이터베이스에 추가된 날짜와 시간입니다.|  
|**설명**|항목에 대한 설명입니다.|  
|**숨김**|사용자가 항목을 볼 수 있으며 사용할 수 있는지 여부를 나타내는 값입니다.|  
|**ID**|보고서 서버 데이터베이스에 있는 항목의 ID입니다.|  
|**ModifiedBy**|보고서 서버 데이터베이스의 항목을 마지막으로 수정한 사용자의 이름입니다.|  
|**ModifiedDate**|사용자가 항목을 마지막으로 수정한 날짜와 시간입니다.|  
|**이름**|보고서 서버 데이터베이스에 있는 항목의 이름입니다.|  
|**경로**|항목의 전체 경로 이름입니다. 보고서 서버 데이터베이스에 있는 항목의 경로에는 최대 260자까지 사용할 수 있습니다.|  
|**크기**|보고서 서버 데이터베이스에 있는 항목의 크기(바이트)입니다.|  
|**형식**|보고서 서버 데이터베이스에 있는 항목의 형식입니다.|  
|**VirtualPath**|보고서 서버 데이터베이스에 있는 항목의 가상 경로입니다. <xref:ReportService2010.CatalogItem.VirtualPath%2A> 속성의 값은 사용자가 항목을 볼 수 있는 경로입니다. 예를 들어, 사용자 개인의 My Reports 폴더에 있는 report1이라는 보고서의 가상 경로는 /My Reports입니다. 항목의 실제 경로는 /Users/username/My Reports입니다.|  
  
## <a name="folder-properties"></a>폴더 속성  
 위에 나열한 항목 속성 외에도 다음 속성이 보고서 서버 데이터베이스의 폴더에 적용됩니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**Reserved**|보고서 서버에서 예약된 폴더에 대해 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 메서드를 통해 반환되는 값입니다. 예약된 폴더에는 Users, My Reports 및 /가 포함됩니다. 예약된 폴더는 수정하거나 제거할 수 없습니다.|  
  
## <a name="report-properties"></a>보고서 속성  
 위에 나열한 항목 속성 외에도 다음 속성이 보고서 서버 데이터베이스의 보고서에 적용됩니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**언어**|보고서에서 사용된 언어입니다. 값은 IETF(Internet Engineering Task Force) RFC1766 사양에 정의된 언어 코드입니다. 첫 번째 부분은 기본 언어를 지정하며 2자로 구성되어 있습니다. 하이픈으로 구분된 두 번째 부분은 해당 언어의 변형 또는 방언을 지정합니다. 보고서 정의에서 `Style` 요소와 연관된 `Body` 요소에 값이 지정되지 않은 경우 기본값은 보고서 서버의 언어입니다.|  
|`ReportProcessingTimeout`|개별 보고서에 대한 제한 시간(초)입니다. 이 값이 설정된 경우 지정된 시간이 경과하면 보고서 서버에서 보고서 처리를 중지합니다. 유효한 값은 `-1`부터 `2`,`147`,`483`,`647`까지입니다. 값이 `-1`이면 보고서 처리 중 시간 제한으로 인한 중지가 발생하지 않습니다. 값이 `null`, 시스템 속성의 값 `ReportProcessingTimeout` 보고서 처리 제한 시간에 사용 됩니다. 기본값은 `null`입니다. 자세한 내용은 [보고서 서버 시스템 속성](reporting-services-properties-report-server-system-properties.md)을 참조하세요.|  
|**ExecutionDate**|보고서에 대해 마지막으로 보고서 스냅숏이 만들어진 날짜와 시간입니다.|  
|**CanRunUnattended**|보고서를 일정에 따라 무인 모드로 실행할 수 있는지 여부를 나타내는 값입니다. 이 속성을 `true`로 설정하면 보고서 매개 변수에 대한 기본값이 정의되고 데이터 원본 자격 증명이 보고서에 저장되거나 자격 증명 검색 옵션이 `None`으로 설정됩니다. 이 속성을 `false`로 설정하면 보고서를 무인 모드로 실행하기 위한 선행 조건이 충족되지 않습니다. 자세한 내용은 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](../../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)을 참조하세요.|  
|**HasParameterDefaultValues**|보고서에 모든 보고서 매개 변수에 대해 설정된 유효한 기본값이 있는지 여부를 나타내는 값입니다. 이 값은 보고서에 보고서 매개 변수가 없는 경우에도 `true`입니다. 이 속성을 `false`로 설정하면 보고서 매개 변수 하나 이상에 유효한 기본값이 없습니다.|  
|**HasDataSourceCredentials**|보고서와 연관된 모든 데이터 원본에 대해 설정된 자격 증명 검색 옵션이 `None`인지 아니면 `Store`인지를 나타내는 값입니다. 이 속성을 `false`로 설정하면 보고서와 연관된 데이터 원본 중 하나에 대해 설정된 자격 증명 검색 옵션이 `Integrated` 또는 `Prompt`입니다.|  
|**IsSnapshotExecution**|보고서가 스냅숏인지 여부를 나타내는 값입니다.|  
|**HasScheduleReadyDataSources**|보고서의 데이터 원본이 예약된 실행을 지원하도록 구성되었는지 여부를 나타내는 값입니다. 이 속성을 `false`로 설정하면 사용자가 보고서를 구독할 수 없습니다.|  
  
## <a name="resource-properties"></a>리소스 속성  
 위에 나열한 항목 속성 외에도 다음 속성이 보고서 서버 데이터베이스의 리소스에 적용됩니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**MimeType**|보고서 서버 데이터베이스에 있는 리소스의 MIME 형식입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [웹 서비스와 .NET Framework를 사용하여 응용 프로그램 빌드](building-applications-using-the-web-service-and-the-net-framework.md)   
 [보고서 서버 웹 서비스](../report-server-web-service.md)   
 [기술 참조&#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
