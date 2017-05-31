---
title: "뷰 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-views
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- views [SQL Server], about views
ms.assetid: ada83c28-e8b7-45d9-b53c-b3d67c8820c8
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ca3c02162484ebf4f12a8b98b1cad2b1aea89c22
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="views"></a>뷰
  뷰는 쿼리에 의해 내용이 정의되는 가상 테이블입니다. 테이블과 같이 뷰는 데이터의 명명된 열과 행 집합으로 구성됩니다. 인덱싱하지 않을 경우 뷰는 데이터베이스에 저장된 데이터 값 집합으로 존재하지 않습니다. 데이터 행과 열은 뷰를 정의하는 쿼리에서 참조하는 테이블에 있으며 뷰가 참조될 때 동적으로 생성됩니다.  
  
 뷰는 뷰에서 참조하는 기본 테이블에 대한 필터 역할을 합니다. 뷰를 정의하는 쿼리는 현재 또는 다른 데이터베이스의 다른 뷰나 하나 이상의 테이블을 기반으로 할 수 있습니다. 분산 쿼리를 사용하면 유형이 다른 여러 원본의 데이터를 사용하는 뷰를 정의할 수도 있습니다. 예를 들어 이 기능은 각각 다른 지역의 데이터가 저장되는 여러 서버에서 구조가 비슷한 데이터를 결합할 때 유용합니다.  
  
 뷰를 사용하면 각 사용자가 데이터베이스를 보는 시각에 초점을 맞추고 데이터 조작을 간소화하며 사용자 지정할 수 있습니다. 뷰는 뷰의 원본이 되는 기본 테이블에 직접 액세스할 수 있는 권한을 부여하지 않고 뷰를 통해 데이터에 액세스하도록 하기 때문에 보안 메커니즘으로 사용할 수 있습니다. 뷰를 사용하면 이전 버전과 호환되는 인터페이스를 통해 스키마가 변경된 기존 테이블을 에뮬레이트할 수 있습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터를 복사하거나 복사해 넣을 때 뷰를 사용하면 성능을 향상시키고 데이터를 분할할 수 있습니다.  
  
## <a name="types-of-views"></a>뷰 유형  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 기본 사용자 정의 뷰의 표준 역할 외에도 데이터베이스에서 특수한 용도로 사용되는 다음과 같은 뷰 유형을 제공합니다.  
  
 인덱싱된 뷰  
 인덱싱된 뷰는 구체화된 뷰이며 즉, 뷰 정의가 계산되고 결과 데이터가 표 형식으로 저장됩니다. 뷰에 고유 클러스터형 인덱스를 만들어 뷰를 인덱싱합니다. 인덱싱된 뷰를 사용하면 일부 유형의 쿼리 성능이 크게 향상될 수 있습니다. 인덱싱된 뷰는 여러 행을 집계하는 쿼리에 가장 적합하며 기본 데이터 집합이 자주 업데이트되는 경우에는 적합하지 않습니다.  
  
 분할 뷰  
 분할된 뷰는 하나 이상의 서버에 있는 여러 멤버 테이블의 수평 분할된 데이터를 조인하여 데이터가 한 테이블에 있는 것처럼 보이게 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 동일한 인스턴스에 있는 멤버 테이블을 조인하는 뷰는 로컬 분할 뷰입니다.  
  
 시스템 뷰  
 시스템 뷰는 카탈로그 메타데이터를 노출합니다. 시스템 뷰를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 또는 인스턴스에 정의된 개체에 대한 정보를 반환할 수 있습니다. 예를 들어 sys.databases 카탈로그 뷰를 쿼리하여 인스턴스에서 사용할 수 있는 사용자 정의 데이터베이스에 대한 정보를 반환할 수 있습니다. 자세한 내용은 [시스템 뷰&#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)를 참조하세요.  
  
## <a name="common-view-tasks"></a>일반 뷰 태스크  
 다음 표에서는 뷰 만들기 또는 수정과 연관된 일반 태스크에 대한 링크를 제공합니다.  
  
|뷰 태스크|항목|  
|----------------|-----------|  
|뷰를 만드는 방법에 대해 설명합니다.|[뷰 만들기](../../relational-databases/views/create-views.md)|  
|인덱싱된 뷰를 만드는 방법에 대해 설명합니다.|[인덱싱된 뷰 만들기](../../relational-databases/views/create-indexed-views.md)|  
|뷰 정의를 수정하는 방법에 대해 설명합니다.|[뷰 수정](../../relational-databases/views/modify-views.md)|  
|뷰를 통해 데이터를 수정하는 방법에 대해 설명합니다.|[뷰를 통해 데이터 수정](../../relational-databases/views/modify-data-through-a-view.md)|  
|뷰를 삭제하는 방법에 대해 설명합니다.|[뷰 삭제](../../relational-databases/views/delete-views.md)|  
|뷰 정의 같은 뷰에 대한 정보를 반환하는 방법에 대해 설명합니다.|[뷰 정보 보기](../../relational-databases/views/get-information-about-a-view.md)|  
|뷰의 이름을 바꾸는 방법에 대해 설명합니다.|[뷰 이름 바꾸기](../../relational-databases/views/rename-views.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [XML 열에서 뷰 만들기](../../relational-databases/xml/create-views-over-xml-columns.md)   
 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)  
  
  
