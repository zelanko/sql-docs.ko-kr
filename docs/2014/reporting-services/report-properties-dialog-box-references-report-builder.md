---
title: 보고서 속성 대화 상자, 참조 (보고서 작성기) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10082"
ms.assetid: 3414c857-8ea6-4fc4-a6d5-b4883c039efa
caps.latest.revision: 11
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 99be366023499607a5798ea202445f2b4a57b6c4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286669"
---
# <a name="report-properties-dialog-box-references-report-builder"></a>보고서 속성 대화 상자, 참조(보고서 작성기)
  **보고서 속성** 대화 상자의 **참조** 를 선택하여 보고서 정의의 식에 사용되는 사용자 지정 또는 다른 외부 어셈블리 및 사용자 지정 클래스 인스턴스에 대한 참조를 추가 또는 제거할 수 있습니다. 사용자 지정 어셈블리는 보고서 작성기의 로컬 모드에서 지원되지 않습니다. 사용자 지정 어셈블리를 사용하는 보고서를 제작하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 보고서 디자이너를 사용하십시오.  
  
## <a name="options"></a>변수  
 **어셈블리 추가 또는 제거**  
 보고서가 참조하는 어셈블리를 나열합니다. 어셈블리는 보고서를 디자인하는 데 사용하는 도구가 설치되어 있는 컴퓨터 및 보고서 서버에 있어야 합니다. 참조의 이름을의 내용과 일치 해야 합니다  **\<CodeModule >** Report Definition Language (.rdl) 파일에 태그를 정확 하 게 합니다.  
  
 **추가**  
 어셈블리를 추가하려면 클릭합니다. **열기** 대화 상자를 열고 보고서 처리 및 식 평가를 완료하는 데 필요한 어셈블리를 선택하려면 줄임표(...) 단추를 클릭합니다.  
  
 **제거**  
 목록에서 어셈블리 참조를 제거하려면 어셈블리 이름을 선택하고 **제거** 단추를 클릭합니다.  
  
 **클래스 추가 또는 제거**  
 보고서에 사용되는 클래스 인스턴스를 나열합니다. 클래스 목록은 인스턴스 기반 멤버만 사용할 수 있고 정적 멤버는 사용할 수 없습니다.  
  
 **추가**  
 클래스 참조를 추가하려면 클릭합니다. **열기** 대화 상자를 열고 보고서 처리 및 식 평가를 완료하는 데 필요한 클래스를 선택하려면 줄임표(...) 단추를 클릭합니다.  
  
 **제거**  
 클래스 인스턴스를 삭제하려면 해당 인스턴스를 선택한 다음 **제거** 단추를 클릭합니다.  
  
 **위로**  
 종속성이 있는 클래스의 경우 이 참조를 목록에서 더 위로 이동할 수 있습니다.  
  
 **아래로**  
 종속성이 있는 클래스의 경우 이 참조를 목록에서 더 아래로 이동할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [대화 상자, 창 및 마법사에 대한 보고서 작성기 도움말](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
  
