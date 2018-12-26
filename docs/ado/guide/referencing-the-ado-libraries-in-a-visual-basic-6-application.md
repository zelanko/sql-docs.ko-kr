---
title: Visual Basic 6 응용 프로그램에서 ADO 라이브러리 참조 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e8e37459c5e48fe817a3bdbb6a824550cf977f66
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696972"
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>Visual Basic 6 애플리케이션에서 ADO 라이브러리 참조
ADO 라이브러리는 Microsoft Visual Basic 6 응용 프로그램을 가져오려면 Visual Basic 프로젝트에 대 한 참조를 설정 해야 합니다.  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>Visual Basic 프로젝트에서 ADO 라이브러리에 대 한 참조를 설정 하려면  
  
1.  새로 만들거나 기존 Visual Basic 프로젝트를 엽니다.  
  
2.  클릭 합니다 **프로젝트** 메뉴 항목 및 선택 **참조 하는 중...**  드롭 다운 메뉴 패널에서 합니다.  
  
3.  **사용 가능한 참조**, 확인란 **Microsoft ActiveX Data Objects *실제* 라이브러리**여기서 ***실제*** 는 최신 버전 번호입니다. 합니다 **위치** 필드 아래에 선택 항목으로 식별 해야 *$installDir\msado15.dll*여기서 *$installDir* 디렉터리의 경로 나타내는 ADO 라이브러리 가 설치 되었습니다.  
  
4.  ADO MD를 사용 하려는 경우 선택 하는 3 단계를 반복 **Microsoft ActiveX Data Objects (다차원) *실제* 라이브러리**합니다. 합니다 **위치** 필드에는이 선택 항목으로 식별 해야 *$installDir\msadomd.dll*합니다.  
  
5.  ADOX 사용 하려는 경우 선택 하는 3 단계를 반복 **Microsoft ADO.ext입니다 *실제* DDL 및 보안을 위한**합니다. 합니다 **위치** 필드에는이 선택 항목으로 식별 해야 *$installDir\msadox.dll*합니다.  
  
6.  클릭 **확인** 참조 설정을 완료 합니다.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 이전 버전의 다음 형식 라이브러리를 복사 또한 ADO를 설치 합니다.  
  
-   *msado27.tlb*, ADO 2.7 Type Library  
  
-   *msado26.tlb*, ADO 2.6 Type Library  
  
-   *msado25.tlb*, ADO 2.5 형식 라이브러리  
  
-   *msado21.tlb*, ADO 2.1 형식 라이브러리  
  
-   *msado20.tlb*, ADO 2.0 형식 라이브러리  
  
 응용 프로그램을 사용 해야 이러한 ADO 라이브러리 이전 버전과 호환성에 대 한 형식 라이브러리의 적절 한 버전을 가져올 해야 합니다. 이 작업을 수행 하려면 이전 섹션의 절차에 따라 대체 *msado15.dll* 하 여 *msadoXX.tlb*여기서 *XX* 가져와야 버전 번호를 나타냅니다.
