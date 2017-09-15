---
title: "ADOX 기본 사항 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADOX, fundamentals
ms.assetid: 954476fc-5f72-4ada-ace5-d9acb27d18f8
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dbc8d415e4dfcaeb4bf7e6a489bd407e87335874
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="adox-fundamentals"></a>ADOX 기본 사항
Microsoft® ActiveX® 데이터 개체 확장 데이터 정의 언어 및 보안 (ADOX)에 대 한는 ADO 개체 및 프로그래밍 모델을 확장 합니다. ADOX 보안 뿐만 아니라 스키마 만들기 및 수정에 대 한 개체를 포함합니다. 스키마 조작 하는 개체 기반 방식 이기 때문에 기본 구문의의 차이 관계 없이 원본 다양 한 데이터에 대해 작동 하는 코드를 작성할 수 있습니다.  
  
 ADOX는 코어 ADO 개체를 도우미 라이브러리입니다. 만들기, 수정 및 삭제 테이블 및 프로시저와 같은 스키마 개체에 대 한 추가 개체를 노출 합니다. 또한 사용자 및 그룹을 유지 관리 권한을 부여 하 고 개체에 사용 권한을 취소 하려면 보안 개체를 포함 합니다.  
  
 ADOX 개발 도구를 사용 하려면 ADOX 형식 라이브러리에 대 한 참조를 설정 해야 합니다. ADOX 라이브러리에 대 한 설명을 "Microsoft ADO 외부 DDL 및 보안에 대 한 합니다." ADOX 라이브러리 파일 이름은 Msadox.dll, 이며 프로그램 ID (ProgID)는 "ADOX"입니다. 라이브러리에 대 한 참조를 설정 하는 방법에 대 한 자세한 내용은 개발 도구의 설명서를 참조 합니다.  
  
 Microsoft OLE DB Provider for Microsoft Jet 데이터베이스 엔진 ADOX를 완벽 하 게 지원 합니다. ADOX의 특정 기능은 데이터 공급자에 따라 지원 되지 않을 수 있습니다.  
  
 이 문서에서는 프로그래밍 언어 및 ADO에 대 한 일반적인 지식이 Microsoft® Visual Basic®에 대 한 실무 지식이 있다고 가정 합니다. ADO에 대 한 자세한 내용은 참조는 [ADO Programmer's Guide](../../../ado/guide/ado-programmer-s-guide.md)합니다. ADOX에 대 한 자세한 개요 내용은 다음 항목을 참조 합니다.  
  
-   [ADOX 개체 모델](../../../ado/reference/adox-api/adox-object-model.md)  
  
-   [ADOX 개체](../../../ado/reference/adox-api/adox-objects.md)  
  
-   [ADOX 컬렉션](../../../ado/reference/adox-api/adox-collections.md)  
  
-   [ADOX 속성](../../../ado/reference/adox-api/adox-properties.md)  
  
-   [ADOX 메서드](../../../ado/reference/adox-api/adox-methods.md)  
  
-   [ADOX 예제](../../../ado/reference/adox-api/adox-code-examples.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ADOX API 참조](../../../ado/reference/adox-api/adox-api-reference.md)   
 [ADOX 코드 예제](../../../ado/reference/adox-api/adox-code-examples.md)   
 [ADOX 컬렉션](../../../ado/reference/adox-api/adox-collections.md)   
 [ADOX 열거 상수](../../../ado/reference/adox-api/adox-enumerated-constants.md)   
 [ADOX 메서드](../../../ado/reference/adox-api/adox-methods.md)   
 [ADOX 개체 모델](../../../ado/reference/adox-api/adox-object-model.md)   
 [ADOX 개체](../../../ado/reference/adox-api/adox-objects.md)   
 [ADOX 속성](../../../ado/reference/adox-api/adox-properties.md)   
 [ADO (다차원) ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [ADO 프로그래머 가이드](../../../ado/guide/ado-programmer-s-guide.md)
