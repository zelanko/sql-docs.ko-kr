---
title: 보고서 속성 대화 상자, 참조 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10530"
- sql12.rtp.rptdesigner.reportproperties.references.f1
ms.assetid: 4639d368-9918-4bb1-9953-7a724ca78dea
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e57e0eb15c8c0ae7e326927ab14493f21c52cc14
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66104303"
---
# <a name="report-properties-dialog-box-references"></a>보고서 속성 대화 상자, 참조
  
  **보고서 속성** 대화 상자의 **참조** 를 선택하여 보고서 정의의 식에 사용되는 사용자 지정 또는 다른 외부 어셈블리 및 사용자 지정 클래스 인스턴스에 대한 참조를 추가 또는 제거할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **어셈블리 추가 또는 제거**  
 보고서가 참조하는 어셈블리를 나열합니다. 어셈블리는 보고서를 디자인하는 데 사용하는 도구가 설치되어 있는 컴퓨터 및 보고서 서버에 있어야 합니다. 참조의 이름은 Report Definition Language 파일 (.rdl)의 ** \<codemodule>** 태그 내용과 정확 하 게 일치 해야 합니다.  
  
 **추가**  
 어셈블리를 추가하려면 클릭합니다. **열기** 대화 상자를 열고 보고서 처리 및 식 평가를 완료 하는 데 필요한 어셈블리를 선택 하려면 줄임표 (...) 단추를 클릭 합니다.  
  
 **Delete**  
 목록에서 어셈블리 참조를 제거하려면 어셈블리 이름을 선택하고 **제거** 단추를 클릭합니다.  
  
 **클래스 추가 또는 제거**  
 보고서에 사용되는 클래스 인스턴스를 나열합니다. 클래스 목록은 인스턴스 기반 멤버만 사용할 수 있고 정적 멤버는 사용할 수 없습니다.  
  
 **추가**  
 클래스 참조를 추가하려면 클릭합니다. **열기** 대화 상자를 열고 보고서 처리 및 식 평가를 완료 하는 데 필요한 클래스를 선택 하려면 줄임표 (...) 단추를 클릭 합니다.  
  
 **Delete**  
 클래스 인스턴스를 삭제하려면 해당 인스턴스를 선택한 다음 **제거** 단추를 클릭합니다.  
  
 **위로**  
 종속성이 있는 클래스의 경우 이 참조를 목록에서 더 위로 이동할 수 있습니다.  
  
 **드롭다운**  
 종속성이 있는 클래스의 경우 이 참조를 목록에서 더 아래로 이동할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 디자이너 &#40;SSRS&#41;의 식에 있는 사용자 지정 코드 및 어셈블리 참조](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [보고서 및 그룹 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](report-design/built-in-collections-report-and-group-variables-references-report-builder.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
