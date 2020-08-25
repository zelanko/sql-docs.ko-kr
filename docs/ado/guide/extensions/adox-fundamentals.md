---
description: ADOX 기본 사항
title: ADOX 기본 사항 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX, fundamentals
ms.assetid: 954476fc-5f72-4ada-ace5-d9acb27d18f8
author: rothja
ms.author: jroth
ms.openlocfilehash: fa7a703f9790ef49961e3324b26c32d757682e4a
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88758813"
---
# <a name="adox-fundamentals"></a>ADOX 기본 사항
Microsoft® ActiveX® 데이터 개체 확장 ADOX (데이터 정의 언어 및 보안)는 ADO 개체 및 프로그래밍 모델에 대 한 확장입니다. ADOX에는 스키마를 만들고 수정할 뿐만 아니라 보안을 위한 개체가 포함 되어 있습니다. 스키마 조작을 위한 개체 기반 방법 이므로 네이티브 구문의 차이점에 관계 없이 다양 한 데이터 원본에 대해 작동 하는 코드를 작성할 수 있습니다.  
  
 ADOX는 핵심 ADO 개체에 대 한 도우미 라이브러리입니다. 테이블, 프로시저 등의 스키마 개체를 만들고 수정 하 고 삭제 하기 위한 추가 개체를 제공 합니다. 또한 사용자 및 그룹을 유지 관리 하 고 개체에 대 한 사용 권한을 부여 하 고 취소 하는 보안 개체를 포함 합니다.  
  
 개발 도구에서 ADOX를 사용 하려면 ADOX 형식 라이브러리에 대 한 참조를 설정 해야 합니다. ADOX 라이브러리에 대 한 설명은 "Microsoft ADO Ext. DDL 및 Security"입니다. ADOX 라이브러리 파일 이름은 Msadox.dll이 고 프로그램 ID (ProgID)는 "ADOX"입니다. 라이브러리에 대 한 참조를 설정 하는 방법에 대 한 자세한 내용은 개발 도구의 설명서를 참조 하세요.  
  
 Microsoft Jet 용 Microsoft OLE DB 공급자 데이터베이스 엔진는 ADOX를 완벽 하 게 지원 합니다. 데이터 공급자에 따라 ADOX의 특정 기능을 지원 하지 않을 수 있습니다.  
  
 이 문서에서는 Microsoft® Visual Basic® 프로그래밍 언어 및 ADO에 대 한 일반적인 지식에 대해 잘 알고 있다고 가정 합니다. ADO에 대 한 자세한 내용은 [Ado 프로그래머 가이드](../ado-programmer-s-guide.md)를 참조 하세요. ADOX에 대 한 자세한 개요 정보는 다음 항목을 참조 하세요.  
  
-   [ADOX 개체 모델](../../reference/adox-api/adox-object-model.md)  
  
-   [ADOX 개체](../../reference/adox-api/adox-objects.md)  
  
-   [ADOX 컬렉션](../../reference/adox-api/adox-collections.md)  
  
-   [ADOX 속성](../../reference/adox-api/adox-properties.md)  
  
-   [ADOX 메서드](../../reference/adox-api/adox-methods.md)  
  
-   [ADOX 예제](../../reference/adox-api/adox-code-examples.md)  
  
## <a name="see-also"></a>관련 항목  
 [ADOX API 참조](../../reference/adox-api/adox-object-model.md?view=sql-server-ver15)   
 [ADOX 코드 예제](../../reference/adox-api/adox-code-examples.md)   
 [ADOX 컬렉션](../../reference/adox-api/adox-collections.md)   
 [ADOX 열거 상수](../../reference/adox-api/adox-enumerated-constants.md)   
 [ADOX 메서드](../../reference/adox-api/adox-methods.md)   
 [ADOX 개체 모델](../../reference/adox-api/adox-object-model.md)   
 [ADOX 개체](../../reference/adox-api/adox-objects.md)   
 [ADOX 속성](../../reference/adox-api/adox-properties.md)   
 [ADO (다차원) (ADO MD)](../multidimensional/ado-multidimensional-ado-md.md)   
 [ADO 프로그래머 가이드](../ado-programmer-s-guide.md)