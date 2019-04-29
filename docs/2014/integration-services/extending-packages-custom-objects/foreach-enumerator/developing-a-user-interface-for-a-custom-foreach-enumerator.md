---
title: 사용자 지정 ForEach 열거자의 사용자 인터페이스 개발 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom user interface [Integration Services], custom foreach enumerators
- custom foreach enumerators [Integration Services], developing custom user interface
ms.assetid: 8aa4aa80-c9ba-42b3-ba87-ae5ea5d3cac3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8965fcda896c67b2ae2e08cde54c679e6504b8b6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62896073"
---
# <a name="developing-a-user-interface-for-a-custom-foreach-enumerator"></a>사용자 지정 ForEach 열거자의 사용자 인터페이스 개발
  기본 클래스의 속성 및 메서드 구현을 재정의하여 사용자 지정 기능을 제공한 후 Foreach 열거자에 대한 사용자 지정 사용자 인터페이스를 만들 수 있습니다. 사용자 지정 사용자 인터페이스를 만들지 않을 경우 사용자는 속성 창에서만 새 사용자 지정 Foreach 열거자를 구성할 수 있습니다.  
  
 사용자 지정 사용자 인터페이스 프로젝트 또는 어셈블리에서는 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI>를 구현하는 클래스를 만듭니다. 이 클래스는 일반적으로 다른 Windows Forms 컨트롤을 호스팅하는 합성 컨트롤을 만드는 데 사용되는 System.Windows.Forms.UserControl에서 파생됩니다. 만든 컨트롤은 **Foreach 루프 편집기**의 **컬렉션** 탭에 있는 **열거자 구성** 영역에 표시됩니다.  
  
> [!IMPORTANT]  
>  [사용자 지정 개체 빌드, 배포 및 디버그](../building-deploying-and-debugging-custom-objects.md)에 설명된 대로 사용자 지정 사용자 인터페이스를 서명 및 빌드하고 전역 어셈블리 캐시에 설치한 후에는 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>의 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A> 속성에서 이 클래스의 정규화된 이름을 지정해야 합니다.  
  
## <a name="coding-the-user-interface-control-class"></a>사용자 인터페이스 컨트롤 클래스 코딩  
  
### <a name="initializing-the-user-interface"></a>사용자 인터페이스 초기화  
 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.Initialize%2A> 메서드를 재정의하여 호스트 개체에 대한 참조와 패키지에 정의된 연결 관리자 및 변수의 컬렉션에 대한 참조를 캐시할 수 있습니다.  
  
### <a name="setting-properties-on-the-user-interface-control"></a>사용자 인터페이스 컨트롤의 속성 설정  
 사용자 인터페이스 클래스를 파생시키는 기본 UserControl 클래스는 다른 Windows Forms 컨트롤을 호스팅하는 합성 컨트롤로 사용됩니다. 이 클래스는 다른 컨트롤을 호스팅하므로 Windows Forms 응용 프로그램에서와 같이 컨트롤을 끌어 놓은 다음 정렬하고 해당 속성을 설정하고 런타임에 해당 이벤트에 응답하여 사용자 지정 인터페이스를 디자인할 수 있습니다.  
  
### <a name="saving-settings"></a>설정 저장  
 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.SaveSettings%2A> 메서드를 재정의하여 사용자가 편집기를 닫을 때 컨트롤에서 선택한 값을 열거자의 속성에 복사할 수 있습니다.  
  
![Integration Services 아이콘 (작은)](../../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 Foreach 열거자 만들기](creating-a-custom-foreach-enumerator.md)   
 [사용자 지정 Foreach 열거자 코딩](coding-a-custom-foreach-enumerator.md)  
  
  
