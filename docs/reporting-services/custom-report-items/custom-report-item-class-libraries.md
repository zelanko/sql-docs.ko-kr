---
title: "사용자 지정 보고서 항목 클래스 라이브러리 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, RDL
- RDL [Reporting Services], custom report items
ms.assetid: f18c5d8f-1d6b-4f0b-8657-c14896c2ce0d
caps.latest.revision: "27"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fbd23c312a441fe7df7b85033e95c96ff2d3a8a0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="custom-report-item-class-libraries"></a>사용자 지정 보고서 항목 클래스 라이브러리
  사용자 지정 보고서 항목은 **Microsoft.ReportDesigner** 네임스페이스의 클래스를 사용합니다. 사용자 지정 보고서 항목 구현에 사용되는 클래스는 두 개의 기본 범주로 그룹화할 수 있습니다. 하나는 사용자 지정 보고서 항목 인프라를 지원하도록 설계된 고유 클래스이고, 다른 하나는 관련 RDL(Report Definition Language) 요소의 기능을 캡슐화하는 관리되는 래퍼 클래스입니다. 이러한 클래스 사용 방법에 대한 코드 예는 [SQL Server Reporting Services 제품 예제(SQL Server Reporting Services Product Samples)](http://go.microsoft.com/fwlink/?LinkId=177889)를 참조하세요.  
  
## <a name="custom-report-item-infrastructure-classes"></a>사용자 지정 보고서 항목 인프라 클래스  
 다음 클래스는 사용자 지정 보고서 항목을 구현하는 데 사용됩니다.  
  
> [!NOTE]  
>  다음 표는 전체 목록이 아니라 각 클래스에 가장 일반적으로 사용되는 속성 및 메서드를 나열한 것입니다.  
  
### <a name="microsoftreportdesignercustomreportitemdesigner"></a>Microsoft.ReportDesigner.CustomReportItemDesigner  
 주 사용자 지정 보고서 항목 클래스입니다. 각 사용자 지정 보고서 항목 구현의 주 클래스는 이 클래스에서 상속되어야 합니다.  
  
#### <a name="public-properties"></a>Public 속성  
  
|||  
|-|-|  
|**이름**|사용자 지정 보고서 항목의 이름입니다.|  
|**형식**|사용자 지정 보고서 항목의 유형입니다.|  
|**CustomData**|디자인 타임에 지정된 사용자 지정 보고서 항목 데이터 속성을 캡슐화하는 <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> 개체입니다.|  
|**CustomProperties**|사용자 지정 보고서 항목에 대한 사용자 지정 속성 컬렉션입니다.|  
|**Height**|사용자 지정 보고서 항목 컨트롤의 높이입니다.|  
|**Width**|사용자 지정 보고서 항목 컨트롤의 너비입니다.|  
|**보고서**|보고서의 데이터 집합 목록과 같은 보고서 수준 속성의 컨테이너입니다.|  
|**AltReportItem**|사용자 지정 보고서 항목 런타임 컨트롤이 지원되지 않는 곳에서 사용하는, 대체 보고서 항목 개체입니다.|  
|**스타일**|사용자 지정 보고서 항목의 스타일 속성입니다.|  
|**Adornment**|컨트롤의 대화형 편집에 사용되는 도구 영역 창입니다.|  
|**Site**|구성 요소의 **사이트**입니다.|  
|**DesignerVerbCollection**|컨트롤의 바로 가기 메뉴를 위한 사용자 지정 동사 배열입니다.|  
  
#### <a name="public-methods"></a>Public 메서드  
  
|||  
|-|-|  
|**BeginEdit**|컨트롤의 대화형 편집을 활성화합니다.|  
|**DoDefaultAction**|컨트롤에서 마우스를 두 번 클릭하거나 Enter 키를 눌렀을 때 호출됩니다.|  
|**EndEdit**|컨트롤의 대화형 편집을 비활성화합니다.|  
|**GetService**|서비스를 나타내는 개체를 반환합니다.|  
|**InitializeNewComponent**|새 사용자 지정 보고서 항목이 만들어질 때 호출됩니다.|  
|**Invalidate**|컨트롤의 전체 화면을 다시 표시합니다.|  
|**OnDragEnter**<br /><br /> **OnDragDrop**|개체를 컨트롤로 끌어올 때 호출됩니다.|  
|**OnPaint**|**Paint** 이벤트에 대한 응답으로 호출됩니다.|  
  
### <a name="microsoftreportdesignercustomreportitemattribute"></a>Microsoft.ReportDesigner.CustomReportItemAttribute  
 사용자 지정 보고서 항목의 유형을 식별하는 데 사용되는 특성입니다. 보고서 디자이너 구성 파일의 **ReportItem** 요소의 \<**Name**> 특성 값과 이름이 일치해야 합니다.  
  
#### <a name="public-methods"></a>Public 메서드  
  
|||  
|-|-|  
|**CustomReportItemAttribute**|CustomReportItemAttribute 개체를 생성합니다.|  
  
### <a name="microsoftreportdesignerlocalizednameattribute"></a>Microsoft.ReportDesigner.LocalizedNameAttribute  
 사용자 지정 보고서 항목 디자이너에 사용할 표시 이름을 지정하는 데 사용되는 특성입니다.  
  
#### <a name="public-methods"></a>Public 메서드  
  
|||  
|-|-|  
|**LocalizedNameAttribute**|LocalizedNameAttribute 개체를 생성합니다.|  
  
### <a name="microsoftreportdesigneradornment"></a>Microsoft.ReportDesigner.Adornment  
 사용자 지정 보고서 항목 디자인 타임 구성 요소에서 **Adornment** 클래스를 사용하여 주 사각형 디자인 화면 바깥에 일정 영역을 제공할 수 있습니다. 이 영역은 마우스 클릭 및 끌어서 놓기 작업과 같은 사용자 인터페이스 이벤트를 처리할 수 있습니다.  
  
#### <a name="public-methods"></a>Public 메서드  
  
|||  
|-|-|  
|**OnShow**|**Adornment**가 활성화될 때 호출됩니다.|  
|**OnHide**|**Adornment**가 비활성화될 때 호출됩니다.|  
|**Paint**|**Paint** 이벤트에 대한 응답으로 호출됩니다.|  
|**OnDragEnter**<br /><br /> **OnDragOver**<br /><br /> **OnDragLeave**<br /><br /> **OnDragDrop**|개체를 **Adornment**로 끌어올 때 호출됩니다.|  
  
### <a name="microsoftreportdesigneradornerservice"></a>Microsoft.ReportDesigner.AdornerService  
 이 클래스는 사용자 지정 보고서 항목에서 사용자 지정 보고서 항목 디자인 타임 구성 요소에 **Adornment** 개체를 지원하기 위해 사용하는 표시 서비스 컬렉션을 제공합니다.  
  
#### <a name="public-properties"></a>Public 속성  
  
|||  
|-|-|  
|**AdornerWindowBounds**|Adorner 창의 경계입니다.|  
|**AdornerWindowRegion**|Adorner 창의 영역입니다.|  
|**AdornerWindowGraphics**|Adorner 창에 대한 그래픽 컨텍스트입니다.|  
  
#### <a name="public-methods"></a>Public 메서드  
  
|||  
|-|-|  
|**ComponentRectInDesignerFrame**|디자이너 프레임 좌표로 변환된 구성 요소의 경계를 반환합니다.|  
|**InvalidateAdorner**|Adorner 창을 무효화합니다.|  
|**PointToAdorner**|Adorner 창 좌표로 변환된 화면 좌표 위치를 반환합니다.|  
  
### <a name="microsoftreportdesignerexpressioneditor"></a>Microsoft.ReportDesigner.ExpressionEditor  
 이 클래스를 사용하여 사용자 지정 보고서 항목 디자인 타임 컨트롤에서 식 편집기를 호출할 수 있습니다.  
  
#### <a name="public-methods"></a>Public 메서드  
  
|||  
|-|-|  
|**EditValue**|주어진 개체 값으로 초기화된 식 편집기를 호출합니다.|  
  
### <a name="microsoftreportdesignerifieldsdataobject"></a>Microsoft.ReportDesigner.IFieldsDataObject  
 이 클래스는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 필드 컬렉션이며 디자인 환경에서 끌어서 놓기 이벤트를 지원하는 데 사용됩니다. **IReportItemDataObject**에서 상속합니다.  
  
#### <a name="public-properties"></a>Public 속성  
  
|||  
|-|-|  
|**DataSetName**|삭제할 필드를 포함하는 데이터 집합의 이름입니다.|  
|**Fields**|삭제될 필드의 컬렉션(**Microsoft.ReportDesigner.Field**)입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 정의 언어&#40;SSRS&#41;](../../reporting-services/reports/report-definition-language-ssrs.md)   
 [사용자 지정 보고서 항목 런타임 구성 요소 만들기](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [사용자 지정 보고서 항목 디자인 타임 구성 요소 만들기](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)  
  
  
