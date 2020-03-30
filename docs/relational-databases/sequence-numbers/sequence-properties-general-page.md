---
title: 시퀀스 속성(일반 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.sequence.general.f1
ms.assetid: 0187f413-cdf0-48a2-b2e6-9b3578cd5811
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b221a39ea46c0bb853aacfbeaa020d67b53ebbca
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68126992"
---
# <a name="sequence-properties-general-page"></a>시퀀스 속성(일반 페이지)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  시퀀스 개체를 만들고 해당 속성을 지정합니다. 시퀀스는 시퀀스를 만들 때 사용된 사양에 따라 숫자 값의 시퀀스를 생성하는 사용자 정의 스키마 바운드 개체입니다. 숫자 값의 시퀀스는 정의된 간격에 따라 오름차순이나 내림차순으로 생성되며, 시퀀스가 모두 사용되면 다시 시작(순환)되도록 구성할 수 있습니다. ID 열과 달리 시퀀스는 특정 테이블과 연결되지 않습니다. 애플리케이션에서는 시퀀스 개체를 참조하여 다음 값을 검색합니다. 시퀀스와 테이블 간의 관계는 애플리케이션에서 제어합니다. 사용자 애플리케이션에서는 시퀀스 개체를 참조하고 여러 행 및 테이블에서 값을 조정합니다.  
  
 행을 삽입할 때 생성되는 ID 열 값과는 달리 애플리케이션에서는 [NEXT VALUE FOR 함수](../../t-sql/functions/next-value-for-transact-sql.md)를 호출하여 행을 삽입하지 않고도 다음 시퀀스 번호를 가져올 수 있습니다. 여러 시퀀스 번호를 한 번에 가져오려면 [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) 를 사용합니다.  
  
 **CREATE SEQUENCE** 및 **NEXT VALUE FOR** 함수를 함께 사용하는 시나리오에 대한 자세한 내용은 [시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)를 참조하세요.  
  
 이 페이지는 개체 탐색기에서 **시퀀스** 를 마우스 오른쪽 단추로 클릭한 다음 **새 시퀀스**를 클릭하거나 기존 시퀀스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭하는 두 가지 방법으로 액세스할 수 있습니다. 기존 시퀀스를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭한 경우에는 옵션을 편집할 수 없습니다. 시퀀스 옵션을 변경하려면 [ALTER SEQUENCE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md) 문을 사용하거나 시퀀스 개체를 삭제한 후 다시 만듭니다.  
  
## <a name="options"></a>옵션  
 **시퀀스 이름**  
 시퀀스 이름을 입력합니다.  
  
 **시퀀스 스키마**  
 이 시퀀스를 소유할 스키마를 지정합니다.  
  
 **데이터 형식**  
 시퀀스는 모든 정수 유형으로 정의할 수 있습니다. 다음 내용이 포함됩니다.  
  
|데이터 형식|범위|  
|---------------|-----------|  
|**tinyint**|0 ~ 255|  
|**smallint**|-32,768 ~ 32,767|  
|**int**|-2,147,483,648 ~ 2,147,483,647|  
|**bigint**|-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807|  
  
-   **decimal** 또는 소수 자릿수가 0인 **numeric**  
  
-   다음 형식 중 하나에 기반을 둔 사용자 정의 데이터 형식(별칭 유형)  
  
 **정밀도**  
 **decimal** 또는 **numeric** 데이터 형식의 경우 전체 자릿수를 지정합니다. 소수 자릿수는 항상 0입니다.  
  
 **시작 값**  
 시퀀스 개체가 반환할 첫 번째 값입니다. **START** 값은 시퀀스 개체의 최대값보다 작거나 같고 최소값보다 크거나 같은 값이어야 합니다. 새 시퀀스 개체의 기본 시작 값은 오름차순 시퀀스 개체에 대해서는 최소값이고, 내림차순 시퀀스 개체에 대해서는 최대값입니다.  
  
 **증가값**  
 각각의 **NEXT VALUE FOR** 함수 호출에 대해 시퀀스 개체의 값을 증가시키거나 감소시키는(음수인 경우) 데 사용되는 값입니다. 증가값이 음수이면 시퀀스 개체가 내림차순이고, 그렇지 않으면 오름차순입니다. 증가값은 0일 수 없습니다.  
  
 **최소값**  
 시퀀스 개체의 경계를 지정합니다. 새 시퀀스 개체의 기본 최소값은 해당 시퀀스 개체의 데이터 형식에 대한 최소값입니다. **tinyint** 형식에 대해서는 0이고 다른 모든 데이터 형식에 대해서는 음수입니다.  
  
 **최대값**  
 시퀀스 개체의 경계를 지정합니다. 새 시퀀스 개체의 기본 최대값은 해당 시퀀스 개체의 데이터 형식에 대한 최대값입니다.  
  
 **제한에 도달하면 시퀀스 순환 다시 시작**  
 최소값 또는 최대값을 초과하는 경우 시퀀스 개체가 최소값 또는 최대값(내림차순 시퀀스 개체의 경우)에서 다시 시작할 수 있도록 하려면 선택합니다.  
  
> [!NOTE]  
>  시작 값이 아니라 최소값/최대값에서 순환이 다시 시작됩니다.  
  
 **캐시 옵션**  
 시퀀스 값 캐시를 만들면 시퀀스 번호를 만드는 데 필요한 디스크 I/O 수를 최소화하여 시퀀스 개체를 사용하는 애플리케이션의 성능을 향상시킬 수 있습니다.  
  
-   기본 캐시 크기 - [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 크기를 선택하지만 선택의 일관성이 보장되지 않습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 는 캐시 크기 계산 방법을 예고 없이 변경할 수 있습니다.  
  
-   캐시 없음 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시퀀스 번호를 캐시하지 않습니다.  
  
-   캐시 크기 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시퀀스 값을 캐시합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 현재 값 및 캐시에 남아 있는 값의 개수를 추적합니다. 따라서 캐시 저장에 필요한 메모리 양은 항상 시퀀스 개체 데이터 형식의 인스턴스 두 개입니다.  
  
 CACHE 옵션을 사용하여 만들 경우 전원 오류와 같은 예기치 않은 종료로 인해 캐시의 시퀀스 번호가 손실될 수 있습니다.  
  
 CREATE SEQUENCE 옵션에 대한 자세한 내용은 [CREATE SEQUENCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 SCHEMA에 대한 **CREATE SEQUENCE**, **ALTER**또는 **CONTROL** 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [sys.sequences&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)  
  
  
