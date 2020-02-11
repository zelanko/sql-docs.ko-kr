---
title: 기본 및 외래 키 제약 조건 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- foreign keys [SQL Server], cascading referential integrity
- FOREIGN KEY constraints
- foreign keys [SQL Server]
- foreign keys [SQL Server], about foreign key constraints
ms.assetid: 31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 45d4cd390e0369d8289ed9e58de01b7a02f752c5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68196744"
---
# <a name="primary-and-foreign-key-constraints"></a>PRIMARY KEY 및 FOREIGN KEY 제약 조건
  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 데이터 무결성을 강제 적용하는 데 사용할 수 있는 두 가지 유형의 제약 조건으로 기본 키와 외래 키가 있습니다. 이들 키는 중요한 데이터베이스 개체입니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [Primary Key 제약 조건](../tables/primary-and-foreign-key-constraints.md#PKeys)  
  
 [Foreign Key 제약 조건](../tables/primary-and-foreign-key-constraints.md#FKeys)  
  
 [관련 작업](../tables/primary-and-foreign-key-constraints.md#Tasks)  
  
##  <a name="PKeys"></a>Primary Key 제약 조건  
 테이블에는 일반적으로 테이블의 각 행을 고유하게 식별하는 값을 가진 열 또는 열 조합이 포함되어 있습니다. 이러한 열이나 열 조합은 테이블의 PK(기본 키)라고 하며 테이블에 엔터티 무결성을 적용합니다. 기본 키 제약 조건은 데이터의 고유성을 보장하므로 자주 ID 열에 정의됩니다.  
  
 테이블에 대해 기본 키 제약 조건을 지정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 기본 키 열에 대해 고유 인덱스를 자동으로 만들어 데이터 고유성을 적용합니다. 또한 쿼리에서 기본 키가 사용되는 경우 이 인덱스를 사용하여 데이터에 빠르게 액세스할 수 있습니다. 기본 키 제약 조건이 두 개 이상의 열에 정의되는 경우 한 열에 중복된 값이 있을 수 있지만 기본 키 제약 조건 정의에 있는 모든 열의 값 조합은 각각 고유해야 합니다.  
  
 다음 그림에서와 같이 **Purchasing.ProductVendor** 테이블의 **ProductID** 및 **VendorID** 열은 이 테이블에 대한 복합 기본 키 제약 조건을 구성합니다. 그 결과 **ProductVendor** 테이블의 모든 열에서 **ProductID**와 **VendorID**의 조합은 고유합니다. 따라서 중복 행을 삽입할 수 없습니다.  
  
 ![복합 PRIMARY KEY 제약 조건](../../database-engine/media/fund04.gif "복합 PRIMARY KEY 제약 조건")  
  
-   테이블은 하나의 기본 키 제약 조건만 포함할 수 있습니다.  
  
-   기본 키는 16개 열을 초과할 수 없으며 총 키 길이가 900바이트를 넘을 수 없습니다.  
  
-   기본 키 제약 조건에 의해 생성된 인덱스 수는 비클러스터형 인덱스 999개, 클러스터형 인덱스 1개인 테이블의 인덱스 수 제한을 초과할 수 없습니다.  
  
-   기본 키 제약 조건에 대해 클러스터형 또는 비클러스터형을 지정하지 않은 경우 테이블에 클러스터형 인덱스가 없으면 클러스터형이 사용됩니다.  
  
-   기본 키 제약 조건 내에서 정의된 모든 열은 NOT NULL로 정의되어야 합니다. NULL 허용 여부를 지정하지 않은 경우에는 기본 키 제약 조건에 참여하는 모든 열의 NULL 허용 여부가 NOT NULL로 설정됩니다.  
  
-   CLR 사용자 정의 형식 열에 기본 키를 정의하는 경우 형식 구현이 이진 순서를 지원해야 합니다.  
  
##  <a name="FKeys"></a>Foreign Key 제약 조건  
 외래 키(FK)는 두 테이블의 데이터 간 연결을 설정하고 강제 적용하여 외래 키 테이블에 저장될 수 있는 데이터를 제어하는 데 사용되는 열입니다. 외래 키 참조에서는 한 테이블의 기본 키 값을 가지고 있는 열을 다른 테이블의 열이 참조할 때 두 테이블 간에 연결이 생성됩니다. 이때 두 번째 테이블에 추가되는 열이 외래 키가 됩니다.  
  
 예를 들어 **Sales.SalesOrderHeader** 테이블에는 **Sales.SalesPerson** 테이블에 대한 외래 키 연결이 생성되는데 이는 판매 주문과 영업 사원 간에 논리적 관계가 있기 때문입니다. 
  **SalesOrderHeader** 테이블의 **SalesPersonID** 열은 **SalesPerson** 테이블의 기본 키 열과 일치합니다. 
  **SalesOrderHeader** 테이블의 **SalesPersonID** 열은 **SalesPerson** 테이블에 대한 외래 키입니다. 이 외래 키 관계를 만들면 **SalesPerson** 테이블에 **SalesPersonID** 값이 없을 경우 **SalesOrderHeader** 테이블에 이 값을 삽입할 수 없습니다.  
  
### <a name="indexes-on-foreign-key-constraints"></a>FOREIGN KEY 제약 조건에 대한 인덱스  
 기본 키 제약 조건과 달리 외래 키 제약 조건을 만들어도 해당 인덱스가 자동으로 생성되지 않습니다. 그러나 외래 키에 대해 인덱스를 수동으로 만들면 다음과 같은 경우 유용합니다.  
  
-   외래 키 열은 쿼리에서 한 테이블의 외래 키 제약 조건 열을 다른 테이블의 기본 또는 고유 키 열과 연결하여 테이블의 데이터를 병합하는 조인에서 자주 사용됩니다. 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 인덱스를 만들어 외래 키 테이블에 있는 관련 데이터를 빠르게 찾을 수 있습니다. 그러나 반드시 인덱스를 만들 필요는 없습니다. 테이블 간에 기본 키 또는 외래 키 제약 조건이 정의되지 않더라도 관련된 두 테이블의 데이터를 결합할 수 있습니다. 그러나 두 테이블 간 외래 키 관계가 설정되면 키를 기준으로 하는 쿼리에서 결합할 때 최적화될 수 있습니다.  
  
-   기본 키 제약 조건이 변경되면 연결된 테이블의 외래 키 제약 조건도 검사합니다.  
  
### <a name="referential-integrity"></a>참조 무결성  
 외래 키 제약 조건의 기본 목적이 외래 키 테이블에 저장되는 데이터를 제어하는 것이지만 기본 키 테이블의 데이터 변경 사항도 제어할 수 있습니다. 예를 들어 한 영업 사원에 대한 행이 **Sales.SalesPerson** 테이블에서 삭제되었는데 이 영업 사원의 ID가 **Sales.SalesOrderHeader** 테이블의 판매 주문에 사용된 경우 두 테이블 간의 관계 무결성이 손상됩니다. **SalesPerson** 테이블의 데이터에 대한 연결이 끊어졌으므로 삭제된 영업 사원의 판매 주문은 **SalesOrderHeader** 테이블에서 고아 항목이 됩니다.  
  
 외래 키 제약 조건은 이런 상황이 발생되지 않도록 합니다. 이 제약 조건은 기본 키 테이블의 데이터를 변경할 때 외래 키 테이블에 있는 데이터로의 연결이 무효화될 가능성이 있으면 그 데이터를 변경하지 못하도록 하여 참조 무결성을 강제 적용합니다. 삭제되거나 변경되는 기본 키 값이 다른 테이블의 외래 키 제약 조건 값과 연결되어 있으면 기본 키 테이블의 행을 삭제하거나 기본 키 값을 변경하려는 동작이 수행되지 않습니다. 외래 키 제약 조건의 행을 제대로 변경하거나 삭제하려면 먼저 외래 키 테이블에 있는 외래 키 데이터를 삭제하거나 변경하여 외래 키를 다른 기본 키 데이터에 연결해야 합니다.  
  
#### <a name="cascading-referential-integrity"></a>연계 참조 무결성  
 연계 참조 무결성 제약 조건을 사용하면 기존 외래 키가 가리키는 키를 사용자가 삭제 또는 업데이트하려 할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 수행할 동작을 정의할 수 있습니다. 다음과 같은 연계 동작을 정의할 수 있습니다.  
  
 NO ACTION  
 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 오류가 발생하며 부모 테이블의 행에 대한 삭제 또는 업데이트 동작이 롤백됩니다.  
  
 CASCADE  
 부모 테이블에서 해당 행이 업데이트되거나 삭제될 때 참조 테이블에서도 해당 행이 업데이트 또는 삭제됩니다. 
  `timestamp` 열이 외래 키 또는 참조되는 키의 일부인 경우에는 CASCADE를 지정할 수 없습니다. INSTEAD OF DELETE 트리거가 있는 테이블에는 ON DELETE CASCADE를 지정할 수 없습니다. INSTEAD OF UPDATE 트리거가 있는 테이블에 대해서는 ON UPDATE CASCADE를 지정할 수 없습니다.  
  
 SET NULL  
 부모 테이블에서 행을 업데이트하거나 삭제하면 해당 외래 키를 구성하는 모든 값이 NULL로 설정됩니다. 이 제약 조건을 실행하려면 외래 키 열이 Null을 허용해야 합니다. INSTEAD OF UPDATE 트리거가 있는 테이블에 대해서는 지정할 수 없습니다.  
  
 SET DEFAULT  
 부모 테이블에서 해당 행을 업데이트하거나 삭제하면 외래 키를 구성하는 모든 값이 기본값으로 설정됩니다. 이 제약 조건을 실행하려면 모든 외래 키 열에 기본 정의가 있어야 합니다. 열이 Null을 허용하고 명시적 기본값이 설정되어 있지 않은 경우 NULL은 해당 열의 암시적 기본값이 됩니다. INSTEAD OF UPDATE 트리거가 있는 테이블에 대해서는 지정할 수 없습니다.  
  
 CASCADE, SET NULL, SET DEFAULT 및 NO ACTION은 서로 참조 관계를 가진 테이블에서 결합될 수 있습니다. 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 NO ACTION을 발견하면 관련된 CASCADE, SET NULL 및 SET DEFAULT 동작을 멈추고 롤백합니다. DELETE 문으로 CASCADE, SET NULL, SET DEFAULT 및 NO ACTION 동작을 결합하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 NO ACTION을 확인하기 전에 모든 CASCADE, SET NULL 및 SET DEFAULT 동작을 적용합니다.  
  
### <a name="triggers-and-cascading-referential-actions"></a>트리거 및 연계 참조 동작  
 연계 참조 동작은 다음과 같은 방식으로 AFTER UPDATE 또는 AFTER DELETE 트리거를 시작합니다.  
  
-   원래 DELETE 또는 UPDATE 문에 의해 직접적으로 시작된 모든 연계 참조 동작이 먼저 수행됩니다.  
  
-   영향을 받는 테이블에 AFTER 트리거가 정의되어 있는 경우 해당 트리거는 모든 연계 동작이 수행된 후에 시작됩니다. 이 트리거는 연계 동작 순서와 반대로 시작됩니다. 단일 테이블에 여러 트리거가 있는 경우 이 테이블에 첫 번째 또는 마지막으로 지정된 트리거가 없다면 임의의 순서로 시작됩니다. 이 시작 순서는 [sp_settriggerorder](/sql/relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql)를 사용하여 지정한 대로 수행됩니다.  
  
-   UPDATE 또는 DELETE 동작의 직접적인 대상인 테이블로부터 여러 연계 체인이 시작되는 경우 이 체인이 각 트리거를 시작하는 순서는 지정되지 않습니다. 그러나 항상 한 체인이 해당 트리거를 모두 시작한 후에 다른 체인이 해당 트리거를 시작합니다.  
  
-   UPDATE 또는 DELETE 동작의 직접적인 대상인 테이블에 대한 AFTER 트리거는 영향을 받는 행이 있는지 여부에 관계 없이 항상 시작됩니다. 이 경우 다른 테이블은 연계 작업에 영향을 받지 않습니다.  
  
-   이전 트리거 중 하나가 다른 테이블에 대해 UPDATE 또는 DELETE 작업을 수행하는 경우 이 동작에 의해 보조 연계 체인이 시작될 수 있습니다. 이러한 보조 체인은 기본 체인의 모든 트리거가 시작된 후에 각 UPDATE 또는 DELETE 작업에서 처리됩니다. 이러한 과정은 나중에 수행되는 UPDATE 또는 DELETE 작업에서 재귀적으로 반복될 수 있습니다.  
  
-   트리거 내에서 CREATE, ALTER, DELETE 또는 기타 DDL(데이터 정의 언어) 작업이 수행되면 DDL 트리거가 시작될 수 있습니다. 그리고 추가 연계 체인과 트리거를 시작하는 DELETE 또는 UPDATE 작업이 뒤이어 수행될 수 있습니다.  
  
-   특정 연계 참조 동작 체인 내에서 오류가 생성되면 오류가 발생하고 해당 체인에서 AFTER 트리거가 시작되지 않으며 체인을 만든 DELETE 또는 UPDATE 작업이 롤백됩니다.  
  
-   INSTEAD OF 트리거가 있는 테이블은 연계 동작을 지정하는 REFERENCES 절도 가질 수 없습니다. 그러나 연계 동작의 대상이 되는 테이블의 AFTER 트리거는 다른 테이블 또는 그 개체에 정의된 INSTEAD OF 트리거를 시작하는 뷰에서 INSERT, UPDATE 또는 DELETE 문을 실행할 수 있습니다.  
  
##  <a name="Tasks"></a> 관련 작업  
 다음 표에서는 기본 키 및 외래 키 제약 조건과 연관된 일반 태스크를 보여 줍니다.  
  
|Task|항목|  
|----------|-----------|  
|기본 키를 만드는 방법에 대해 설명합니다.|[기본 키 만들기](../tables/create-primary-keys.md)|  
|기본 키를 삭제하는 방법에 대해 설명합니다.|[기본 키 삭제](../tables/delete-primary-keys.md)|  
|기본 키를 수정하는 방법에 대해 설명합니다.|[기본 키 수정](../tables/modify-primary-keys.md)|  
|외래 키 관계를 만드는 방법에 대해 설명합니다.|[외래 키 관계 만들기](../tables/create-foreign-key-relationships.md)|  
|외래 키 관계를 수정하는 방법에 대해 설명합니다.|[외래 키 관계 수정](../tables/modify-foreign-key-relationships.md)|  
|외래 키 관계를 삭제하는 방법에 대해 설명합니다.|[외래 키 관계 삭제](../tables/delete-foreign-key-relationships.md)|  
|외래 키 속성을 보는 방법에 대해 설명합니다.|[외래 키 속성 보기](../tables/view-foreign-key-properties.md)|  
|복제에 대한 외래 키 제약 조건을 사용하지 않도록 설정하는 방법에 대해 설명합니다.|[복제할 때 FOREIGN KEY 제약 조건 비활성화](../tables/disable-foreign-key-constraints-for-replication.md)|  
|INSERT 또는 UPDATE 문 중에 외래 키 제약 조건을 사용하지 않도록 설정하는 방법에 대해 설명합니다.|[NSERT 및 UPDATE 문에서 FOREIGN KEY 제약 조건 사용 안 함](../tables/disable-foreign-key-constraints-with-insert-and-update-statements.md)|  
  
  
