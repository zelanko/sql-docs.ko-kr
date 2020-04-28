---
title: ADO MD 기본 사항 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, fundamentals
ms.assetid: f6a20d9f-c1ab-474c-b9f3-82277e2a126d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 690c7b58c336596485b9ade77f0c02928853cd2d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923208"
---
# <a name="ado-md-fundamentals"></a>ADO MD 기본 사항
Microsoft® ActiveX® 데이터 개체 (다차원) (ADO MD)를 사용 하면 Microsoft Visual Basic®, Microsoft Visual C++® 등의 언어에서 다차원 데이터에 쉽게 액세스할 수 있습니다. ADO MD은 Microsoft ActiveX ADO (® Data Objects)를 확장 하 여 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) 및 [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체와 같은 다차원 데이터에 특정 한 개체를 포함 합니다. ADO MD 다차원 스키마를 찾아보고, 큐브를 쿼리하고, 결과를 검색할 수 있습니다.  
  
 ADO와 마찬가지로 ADO MD 기본 OLE DB 공급자를 사용 하 여 데이터에 대 한 액세스 권한을 얻습니다. ADO MD를 사용 하려면 공급자가 OLAP 사양 OLE DB에 정의 된 대로 .MDP (multidimensional data provider) 여야 합니다. .MDP는 테이블 형식 뷰가 아닌 다차원 뷰로 데이터를 표시 합니다 .이는 TDP (테이블 형식 데이터 공급자)가 데이터를 표시 하는 방법입니다. 공급자가 지 원하는 특정 구문 및 동작에 대 한 자세한 내용은 OLAP OLE DB 공급자에 대 한 설명서를 참조 하세요.  
  
 이 문서에서는 Visual Basic 프로그래밍 언어에 대해 잘 알고 있는 것으로 가정 하 고 ADO 및 OLAP에 대해 일반적으로 알고 있다고 가정 합니다. 자세한 내용은 [ADO 프로그래머 가이드](../../../ado/guide/ado-programmer-s-guide.md) 및 [OLAP (온라인 분석 처리)에 대 한 OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms717005.aspx)를 참조 하세요.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [다차원 스키마 및 데이터 개요](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)  
  
-   [다차원 데이터 작업](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)  
  
-   [ADO MD에서 ADO 사용](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)  
  
-   [ADO MD를 사용한 프로그래밍](../../../ado/guide/multidimensional/programming-with-ado-md.md)  
  
## <a name="see-also"></a>참고 항목  
 [ADO MD 개체 모델](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO 프로그래머 가이드](../../../ado/guide/ado-programmer-s-guide.md)   
 [데이터 정의 언어 및 보안을 위한 ADO 확장 (ADOX)](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [다차원 스키마 및 데이터 개요](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [ADO MD를 사용한 프로그래밍](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [ADO MD와 함께 ADO 사용](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [다차원 데이터 작업](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
