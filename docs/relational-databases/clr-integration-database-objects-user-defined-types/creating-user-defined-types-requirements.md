---
title: 사용자 정의 형식 요구 사항 | Microsoft Docs
description: 이 문서에서는 SQL Server에 설치할 UDT를 만들 때 수행 해야 하는 중요 한 디자인 결정에 대해 설명 합니다.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- UDTs [CLR integration], requirements
- serialization
- Native serialization format [CLR integration]
- attributes [CLR integration]
- XML serialization [CLR integration]
- user-defined types [CLR integration], requirements
- user-defined serialization [CLR integration]
- user-defined types [CLR integration], Native serialization
- UDTs [CLR integration], Native serialization
ms.assetid: bedc3372-50eb-40f2-bcf2-d6db6a63b7e6
author: rothja
ms.author: jroth
ms.openlocfilehash: 2b19a9179cba2225a2209255ce48220669e4bbef
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81486982"
---
# <a name="creating-user-defined-types---requirements"></a>사용자 정의 형식 만들기 - 요구 사항
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치할 UDT (사용자 정의 형식)를 만들 때 몇 가지 중요 한 디자인 결정을 내려야 합니다. 대부분의 UDT는 구조로 만드는 것이 좋지만 클래스로 만드는 방법도 고려해 볼 수 있습니다. UDT 정의가 UDT 생성 사양에 맞아야만 UDT 정의를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 등록할 수 있습니다.  
  
## <a name="requirements-for-implementing-udts"></a>UDT 구현을 위한 요구 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 UDT를 실행하려면 UDT 정의에서 다음 요구 사항을 구현해야 합니다.  
  
 UDT는 **SqlUserDefinedTypeAttribute**를 지정 해야 합니다. **SerializableAttribute** 사용은 선택 사항 이지만 권장 됩니다.  
  
-   UDT는 public **static** (Visual Basic에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] **공유** ) **Null** 메서드를 만들어 클래스나 구조체에서 **SqlTypes** 을 구현 해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 기본적으로 Null을 인식합니다. 이 작업은 UDT를 실행하는 코드에서 Null 값을 인식할 수 있도록 하는 데 필요합니다.  
  
-   UDT에는의 구문 분석을 지 원하는 공용 **정적** (또는 **공유**) **구문 분석** 메서드와 개체의 문자열 표현으로 변환 하기 위한 공용 **ToString** 메서드가 포함 되어야 합니다.  
  
-   사용자 정의 직렬화 형식의 UDT는 **IBinarySerialize** 인터페이스를 구현 하 고 **읽기** 및 **쓰기** 메서드를 제공 해야 합니다.  
  
-   UDT는 XmlIgnore를 **구현 해야 합니다. 또는**표준 Serialization이 필요한 경우 모든 public 필드와 속성은 xml Serializable 또는 **XmlIgnore** 특성을 사용 하 여 데코레이팅된 형식 이어야 합니다.  
  
-   UDT 개체의 직렬화가 하나만 있어야 합니다. 직렬화 또는 역직렬화 루틴에서 특정 개체의 표현을 두 개 이상 인식하면 유효성 검사가 실패합니다.  
  
-   **SqlUserDefinedTypeAttribute** 는 바이트 순서로 데이터를 비교 하려면 **true** 여야 합니다. IComparable 인터페이스를 구현 하지 않고 **SqlUserDefinedTypeAttribute. IsByteOrdered** 가 **false**인 경우 바이트 순서 비교가 실패 합니다.  
  
-   클래스에 정의된 UDT에는 인수를 사용하지 않는 공용 생성자가 있어야 합니다. 오버로드된 추가 클래스 생성자를 만들 수도 있습니다.  
  
-   UDT가 데이터 요소를 공용 필드나 속성 프로시저로 표시해야 합니다.  
  
-   공개 이름은 128 자 보다 길 수 없으며 [데이터베이스 식별자](../../relational-databases/databases/database-identifiers.md)에 정의 된 식별자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 명명 규칙을 따라야 합니다.  
  
-   **sql_variant** 열은 UDT의 인스턴스를 포함할 수 없습니다.  
  
-   상속된 멤버는 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 액세스할 수 없습니다. 그 이유는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유형 시스템에서 UDT 간의 상속 계층을 인식하지 못하기 때문입니다. 그러나 클래스를 구성할 때는 상속을 사용할 수 있으며 관리 코드를 사용한 형식 구현에서 이러한 메서드를 호출할 수 있습니다.  
  
-   클래스 생성자를 제외하고는 멤버를 오버로드할 수 없습니다. 오버로드된 메서드를 만드는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 어셈블리를 등록하거나 형식을 만들 때는 오류가 발생하지 않습니다. 오버로드된 메서드는 형식이 만들어질 때가 아니라 런타임에 검색됩니다. 오버로드된 메서드를 호출하지 않는 한 오버로드된 메서드가 클래스 내에 존재할 수 있으며, 오버로드된 메서드를 호출하면 오류가 발생합니다.  
  
-   **Static** (또는 **Shared**) 멤버는 상수로 선언 하거나 읽기 전용으로 선언 해야 합니다. 정적 멤버는 변경할 수 없습니다.  
  
-   **SqlUserDefinedTypeAttribute MaxByteSize** 필드를-1로 설정 하면 직렬화 된 UDT가 LOB (large object) 크기 제한 (현재는 2gb) 만큼 클 수 있습니다. UDT의 크기는 **MaxByteSized** 필드에 지정 된 값을 초과할 수 없습니다.  
  
> [!NOTE]  
>  서버에서는 비교를 수행 하는 데 사용 되지 않지만, 단일 메서드인 **CompareTo**를 노출 하는 **system.string 인터페이스를** 선택적으로 구현할 수 있습니다. 이 인터페이스는 UDT 값을 정확하게 비교하거나 정렬해야 하는 경우에 클라이언트 쪽에서 사용됩니다.  
  
## <a name="native-serialization"></a>네이티브 직렬화  
 만들려는 UDT의 종류에 따라 UDT에 적합한 직렬화 특성을 선택해야 합니다. **네이티브** serialization 형식은를 사용 하 여 디스크에 UDT의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 효율적인 기본 표현을 저장할 수 있는 매우 간단한 구조를 활용 합니다. UDT가 단순 하 고 다음 형식의 필드만 포함 하는 경우 **네이티브** 형식을 권장 합니다.  
  
 **bool**, **byte**, **sbyte**, **short**, **ushort**, **int**, **uint**, **long**, **ulong**, **float**, **double**, **SqlByte**, **SqlInt16**, **SqlInt32**, **SqlInt64**, **SqlDateTime**, **SqlSingle**, **SqlDouble**, **SqlMoney**, **SqlBoolean**  
  
 위 형식의 필드로 구성 되는 값 형식은 **네이티브** 형식 (예: Visual c #의 **구조체** ), (또는 Visual Basic에서 알려진 **구조** )에 적합 합니다. 예를 들어 **네이티브** 직렬화 형식으로 지정 된 udt에는 **네이티브** 형식으로도 지정 된 다른 udt의 필드가 포함 될 수 있습니다. UDT 정의가 좀 더 복잡 하 고 위의 목록에 없는 데이터 형식을 포함 하는 **경우에는 사용자 지정 직렬화 형식을** 대신 지정 해야 합니다.  
  
 **네이티브** 형식에는 다음과 같은 요구 사항이 있습니다.  
  
-   형식은 **SqlUserDefinedTypeAttribute. MaxByteSize**에 대 한 값을 지정 하지 않아야 합니다.  
  
-   모든 필드를 직렬화할 수 있어야 합니다.  
  
-   UDT가 구조가 아닌 클래스에 정의 되어 있는 경우 **T e m StructLayoutAttribute** 를 **StructLayout** 로 지정 해야 합니다. 이 특성은 데이터 필드의 물리적 레이아웃을 제어하며 멤버를 멤버가 실제로 나타나는 순서대로 배치하는 데 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 특성을 사용하여 값이 여러 개 포함된 UDT의 필드 순서를 결정합니다.  
  
 **네이티브** 직렬화를 사용 하 여 정의 된 udt의 예는 [사용자 정의 형식 코딩](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)의 Point UDT를 참조 하세요.  
  
## <a name="userdefined-serialization"></a>UserDefined 직렬화  
 **SqlUserDefinedTypeAttribute** 특성에 대 한 자동 설치 형식 설정은 개발자에 게 이진 형식에 대 한 모든 권한을 **제공 합니다.** **형식** 특성 속성을 사용자 **정의**로 지정할 경우 코드에서 다음을 수행 해야 합니다.  
  
-   선택적 **IsByteOrdered** attribute 속성을 지정 합니다. 기본 값은 **false**입니다.  
  
-   **SqlUserDefinedTypeAttribute**의 **MaxByteSize** 속성을 지정 합니다.  
  
-   **IBinarySerialize** 인터페이스를 구현 하 여 UDT에 대 한 **읽기** 및 **쓰기** 메서드를 구현 하는 코드를 작성 합니다.  
  
 사용자 지정 직렬화를 사용 하 여 정의 **된 udt** 의 예는 [사용자 정의 형식 코딩](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)의 통화 UDT를 참조 하세요.  
  
> [!NOTE]  
>  UDT 필드를 인덱싱하려면 UDT 필드에 네이티브 직렬화를 사용하거나 필드를 지속형 필드로 만들어야 합니다.  
  
## <a name="serialization-attributes"></a>직렬화 특성  
 특성은 직렬화를 사용하여 UDT의 스토리지 표현을 생성하고 UDT를 값으로 클라이언트에 전송하는 방법을 결정합니다. UDT를 만들 때 **SqlUserDefinedTypeAttribute** 를 지정 해야 합니다. **SqlUserDefinedTypeAttribute** 특성은 클래스가 udt 임을 나타내며 udt에 대 한 저장소를 지정 합니다. 필요 하지 않지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **serialize** 할 수 있는 특성을 지정할 수 있습니다.  
  
 **SqlUserDefinedTypeAttribute** 에는 다음과 같은 속성이 있습니다.  
  
 **형식**  
 UDT의 데이터 **형식에 따라**네이티브 또는 **기본** 설정으로 사용할 수 있는 serialization 형식을 지정 합니다.  
  
 **IsByteOrdered**  
 에서 **Boolean** UDT에 대 한 이진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 비교를 수행 하는 방법을 결정 하는 부울 값입니다.  
  
 **IsFixedLength**  
 이 UDT의 모든 인스턴스 길이가 같은지 여부를 나타냅니다.  
  
 **MaxByteSize**  
 인스턴스의 최대 크기(바이트)입니다. 사용자 **지정 직렬화 형식** 으로 **MaxByteSize** 를 지정 해야 합니다. 사용자 정의 serialization이 지정 된 UDT의 경우 **MaxByteSize** 는 사용자가 정의한 대로 직렬화 된 형식으로 udt의 전체 크기를 나타냅니다. **MaxByteSize** 의 값은 1에서 8000 사이 여야 합니다. 그렇지 않으면-1로 설정 하 여 UDT가 8000 바이트 보다 큰지 (총 크기는 최대 LOB 크기를 초과할 수 없음). 10**자 (system.string**) 문자열의 속성을 사용 하는 UDT를 고려 합니다. BinaryWriter를 사용 하 여 UDT를 serialize 하는 경우 직렬화 된 문자열의 총 크기는 22 바이트 (유니코드 UTF-16 문자인 경우 2 바이트, 최대 문자 수로 곱하고, 이진 스트림을 serialize 하 여 발생 하는 2 개의 제어 바이트)입니다. 따라서 **MaxByteSize**의 값을 결정할 때 직렬화 된 UDT의 총 크기를 이진 형식으로 직렬화 된 데이터의 크기와 serialization에 의해 발생 하는 오버 헤드로 간주 해야 합니다.  
  
 **ValidationMethodName**  
 UDT의 인스턴스가 유효한지 여부를 검사하는 데 사용되는 메서드의 이름입니다.  
  
### <a name="setting-isbyteordered"></a>IsByteOrdered 설정  
 IsByteOrdered 속성이 **true**로 설정 된 경우 직렬화 된 이진 데이터를 정보의 의미 정렬에 사용할 수 있도록 보장 하는 것이 **SqlUserDefinedTypeAttribute.** 따라서 바이트 정렬된 UDT 개체의 각 인스턴스에는 직렬화된 표현이 하나만 포함될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 직렬화된 바이트에 대한 비교 작업이 수행되면 그 결과는 동일한 비교 작업이 관리 코드에서 수행된 결과와 같아야 합니다. **IsByteOrdered** 가 **true**로 설정 된 경우에도 다음 기능이 지원 됩니다.  
  
-   이 형식의 열에 인덱스를 만드는 기능  
  
-   이 형식의 열에 CHECK 및 UNIQUE 제약 조건과 기본 키 및 외래 키를 만드는 기능  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY, GROUP BY 및 PARTITION BY 절을 사용하는 기능. 이 경우 형식의 이진 표현이 순서를 결정하는 데 사용됩니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 비교 연산자를 사용하는 기능  
  
-   이 형식의 계산 열을 유지하는 기능  
  
 **IsByteOrdered** 가 **true**로 설정 된 경우에는 **네이티브 및 기본** serialization 형식 **모두에서 다음과** 같은 비교 연산자를 지원 합니다.  
  
-   같음(=)  
  
-   같지 않음(!=)  
  
-   보다 큼(>)  
  
-   보다 작음(\<)  
  
-   크거나 같음(>=)  
  
-   작거나 같음(<=)  
  
### <a name="implementing-nullability"></a>Null 허용 여부 구현  
 어셈블리의 특성을 올바르게 지정하는 것 외에도 클래스는 Null 허용 여부를 지원해야 합니다. 로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로드 되는 udt는 null을 인식 하지만 udt에서 null 값을 인식 하려면 클래스에서 **inullable** 인터페이스를 구현 해야 합니다. UDT에서 null 허용 여부를 구현 하는 방법에 대 한 자세한 내용 및 예제는 [사용자 정의 형식 코딩](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)을 참조 하세요.  
  
### <a name="string-conversions"></a>문자열 변환  
 UDT와의 문자열 변환을 지원 하려면 클래스에서 **Parse** 메서드와 **ToString** 메서드를 제공 해야 합니다. **Parse** 메서드를 사용 하면 문자열을 UDT로 변환할 수 있습니다. **Static** 으로 선언 되 고 (또는 Visual Basic에서 **공유** 됨) **SqlString**형식의 매개 변수를 사용 해야 합니다. **구문 분석** 및 **ToString** 메서드를 구현 하는 방법에 대 한 자세한 내용 및 예제는 [사용자 정의 형식 코딩](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)을 참조 하세요.  
  
## <a name="xml-serialization"></a>XML 직렬화  
 Udt는 XML serialization에 대 한 계약을 준수 하 여 **xml** 데이터 형식으로의 변환을 지원 해야 합니다. System.xml **네임 스페이스** 는 개체를 Xml 형식 문서 또는 스트림으로 serialize 하는 데 사용 되는 클래스를 포함 합니다. XML serialization 및 deserialization에 대 한 사용자 지정 서식을 제공 하는 **IXmlSerializable** 인터페이스를 사용 하 여 **xml** serialization을 구현 하도록 선택할 수 있습니다.  
  
 Xml 직렬화는 UDT에서 **xml**로의 명시적 변환을 수행 하는 것 외에도 다음 작업을 수행할 수 있습니다.  
  
-   **Xml** 데이터 형식으로 변환한 후 UDT 인스턴스의 값에 대해 **Xquery** 를 사용 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 네이티브 XML 웹 서비스를 사용하여 매개 변수가 있는 쿼리 및 웹 메서드에서 UDT를 사용합니다.  
  
-   UDT를 사용하여 대량 로드된 XML 데이터를 받습니다.  
  
-   UDT 열이 있는 테이블이 포함된 데이터 세트을 직렬화합니다.  
  
 FOR XML 쿼리에서는 UDT가 직렬화되지 않습니다. Udt의 XML serialization을 표시 하는 FOR XML 쿼리를 실행 하려면 각 UDT 열을 SELECT 문의 **xml** 데이터 형식으로 명시적으로 변환 합니다. 열을 **varbinary**, **varchar**또는 **nvarchar**로 명시적으로 변환할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [사용자 정의 형식 만들기](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
