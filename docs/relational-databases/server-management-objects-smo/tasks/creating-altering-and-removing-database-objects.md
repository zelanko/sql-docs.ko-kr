---
description: 데이터베이스 개체 생성, 변경 및 제거
title: 데이터베이스 개체 작업
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f2ae7dbbfc762ed342ddc085afcb799f9b292966
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468504"
---
# <a name="creating-altering-and-removing-database-objects"></a>데이터베이스 개체 생성, 변경 및 제거
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  SMO 개체를 만드는 단계는 다음과 같습니다.  
  
1.  개체의 인스턴스를 만듭니다.  
  
2.  개체 속성을 설정합니다.  
  
3.  자식 개체의 인스턴스를 만듭니다.  
  
4.  자식 개체 속성을 설정합니다.  
  
5.  개체를 만듭니다.  

 SMO 애플리케이션에서 SMO 개체의 인스턴스를 만들 때 이러한 인스턴스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Create **메서드가 실행되기 전까지는** 인스턴스에 존재하지 않습니다. 그러나 모든 개별 개체에 대해 **Create** 메서드를 실행할 필요는 없습니다. 개체에 자식 개체 집합이 있는 경우 부모 개체만 **Create** 메서드를 실행하면 됩니다. 예를 들어 테이블에 한 개 이상의 열이 있어야 한다는 테이블 정의가 있습니다. 또한 열은 테이블 없이 따로 존재할 수 없습니다. 테이블과 테이블의 열은 상호 종속 관계입니다.  
  
 <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A> 메서드를 사용하여 개체를 변경할 수 있습니다. 개체 컬렉션 중 하나에 자식 개체를 추가하거나 속성 값을 변경하는 등의 개체에 대한 여러 변경 작업은 모두 일괄 처리되고 하나의 작업으로 실행됩니다. **Alter** 메서드를 사용하면 네트워크 트래픽을 줄이고 전반적인 성능을 개선할 수 있습니다.  
  
 개체 및 처음 개체를 만들 때 필요했던 모든 상호 종속 자식 개체를 제거하려면 **Drop** 문을 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SMO 개체 모델](../../../relational-databases/server-management-objects-smo/smo-object-model.md)  
  
  
