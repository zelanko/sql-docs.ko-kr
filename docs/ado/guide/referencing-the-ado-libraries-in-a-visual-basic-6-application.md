---
title: "Visual Basic 6 응용 프로그램에서 ADO 라이브러리 참조 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: "“drivers”"
ms.topic: article
dev_langs: VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eee5dea5945d48b4fd9a2d40380c61c632d02410
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>Visual Basic 6 응용 프로그램에서 ADO 라이브러리 참조
ADO 라이브러리는 Microsoft Visual Basic 6 응용 프로그램을 가져오려면 Visual Basic 프로젝트에 대 한 참조를 설정 해야 합니다.  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>Visual Basic 프로젝트에서 ADO 라이브러리에 대 한 참조를 설정 하려면  
  
1.  새로 만들거나 기존 Visual Basic 프로젝트를 엽니다.  
  
2.  클릭는 **프로젝트** 메뉴 항목을 다음 선택 **참조 중...**  드롭 다운 메뉴 패널에서 합니다.  
  
3.  **사용 가능한 참조**에 대 한 확인란 **Microsoft ActiveX Data Objects *실제* 라이브러리**여기서 ***실제*** 최신을 나타냅니다. 버전 번호입니다. **위치** 아래 필드에 선택 항목으로 식별 해야 *$installDir\msado15.dll*여기서 *$installDir* 는 디렉터리의 경로 나타내는 ADO 라이브러리 가 설치 되었습니다.  
  
4.  ADO MD를 사용 하려는 경우 선택 하는 3 단계를 반복 **Microsoft ActiveX Data Objects (다차원) *실제* 라이브러리**합니다. **위치** 필드에는이 선택 항목으로 식별 해야 *$installDir\msadomd.dll*합니다.  
  
5.  ADOX 사용 하려는 경우 선택 하는 3 단계를 반복 **Microsoft ADO 외부 *실제* DDL 및 보안을 위한**합니다. **위치** 필드에는이 선택 항목으로 식별 해야 *$installDir\msadox.dll*합니다.  
  
6.  클릭 **확인** 에 대 한 참조를 설정 합니다.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 이전 버전의 다음과 같은 형식 라이브러리에도 복사 ADO 설치:  
  
-   *msado27.tlb*, ADO 2.7 형식 라이브러리  
  
-   *msado26.tlb*, ADO 2.6 형식 라이브러리  
  
-   *msado25.tlb*, ADO 2.5 형식 라이브러리  
  
-   *msado21.tlb*, ADO 2.1 형식 라이브러리  
  
-   *msado20.tlb*, ADO 2.0 형식 라이브러리  
  
 응용 프로그램 이전 버전과 호환성에 속하는 이유로 이러한 ADO 라이브러리를 사용 해야, 형식 라이브러리의 적절 한 버전을 가져와야 합니다. 이 수행 하려면 이전 섹션의 절차에 따라 대체 *msado15.dll* 여 *msadoXX.tlb*여기서 *XX* 가져와야 버전 번호를 나타냅니다.
