---
title: 사용자 정의 형식 요구 사항을 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6d4bccc8ae83d25f848011421d057ad8cb0a7016
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="creating-user-defined-types---requirements"></a>사용자 정의 형식-요구 사항 작성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  사용자 정의 형식 (UDT)에 설치를 만들 때 몇 가지 중요 한 디자인 결정을 내려야 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 대부분의 UDT는 구조로 만드는 것이 좋지만 클래스로 만드는 방법도 고려해 볼 수 있습니다. UDT 정의가 UDT 생성 사양에 맞아야만 UDT 정의를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 등록할 수 있습니다.  
  
## <a name="requirements-for-implementing-udts"></a>UDT 구현을 위한 요구 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 UDT를 실행하려면 UDT 정의에서 다음 요구 사항을 구현해야 합니다.  
  
 UDT를 지정 해야 합니다는 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**합니다. 사용은 **System.SerializableAttribute** 선택 사항 이지만 권장 됩니다.  
  
-   UDT를 구현 해야 합니다는 **System.Data.SqlTypes.INullable** 만들어 공용 구조체 또는 클래스에서 인터페이스 **정적** (**Shared** 에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual 기본) **Null** 메서드. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 기본적으로 Null을 인식합니다. 이 작업은 UDT를 실행하는 코드에서 Null 값을 인식할 수 있도록 하는 데 필요합니다.  
  
-   UDT에서 공용 있어야 합니다. **정적** (또는 **Shared**) **구문 분석** from, 구문 분석을 지 원하는 메서드 및 공용 **ToString** 에 대 한 메서드 개체의 문자열 표현으로 변환합니다.  
  
-   사용자 정의 직렬화 형식으로 UDT를 구현 해야 합니다는 **System.Data.IBinarySerialize** 인터페이스를 제공는 **읽기** 및 **쓰기** 메서드.  
  
-   UDT를 구현 해야 **System.Xml.Serialization.IXmlSerializable**, 또는 XML serializable 또는으로 데코 레이트 된 형식의 모든 public 필드와 속성이 있어야는 **XmlIgnore** 특성 경우 표준 직렬화 재정의가 필요 합니다.  
  
-   UDT 개체의 직렬화가 하나만 있어야 합니다. 직렬화 또는 역직렬화 루틴에서 특정 개체의 표현을 두 개 이상 인식하면 유효성 검사가 실패합니다.  
  
-   **SqlUserDefinedTypeAttribute.IsByteOrdered** 해야 **true** 바이트 순서로 데이터를 비교 합니다. IComparable 인터페이스가 구현 되지 않은 경우 및 **SqlUserDefinedTypeAttribute.IsByteOrdered** 은 **false**, 바이트 순서 비교가 실패 합니다.  
  
-   클래스에 정의된 UDT에는 인수를 사용하지 않는 공용 생성자가 있어야 합니다. 오버로드된 추가 클래스 생성자를 만들 수도 있습니다.  
  
-   UDT가 데이터 요소를 공용 필드나 속성 프로시저로 표시해야 합니다.  
  
-   공개 이름은 128 자 보다 길 수 없습니다 하며을 준수 해야 합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 정의 된 식별자에 대 한 명명 규칙 [데이터베이스 식별자](../../relational-databases/databases/database-identifiers.md)합니다.  
  
-   **sql_variant** 열 UDT의 인스턴스를 사용할 수 없습니다.  
  
-   상속된 멤버는 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 액세스할 수 없습니다. 그 이유는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유형 시스템에서 UDT 간의 상속 계층을 인식하지 못하기 때문입니다. 그러나 클래스를 구성할 때는 상속을 사용할 수 있으며 관리 코드를 사용한 형식 구현에서 이러한 메서드를 호출할 수 있습니다.  
  
-   클래스 생성자를 제외하고는 멤버를 오버로드할 수 없습니다. 오버로드된 메서드를 만드는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 어셈블리를 등록하거나 형식을 만들 때는 오류가 발생하지 않습니다. 오버로드된 메서드는 형식이 만들어질 때가 아니라 런타임에 검색됩니다. 오버로드된 메서드를 호출하지 않는 한 오버로드된 메서드가 클래스 내에 존재할 수 있으며, 오버로드된 메서드를 호출하면 오류가 발생합니다.  
  
-   모든 **정적** (또는 **Shared**) 선언 된 상수 또는 읽기 전용으로 멤버 여야 합니다. 정적 멤버는 변경할 수 없습니다.  
  
-   경우는 **SqlUserDefinedTypeAttribute.MaxByteSize** 필드-1로 설정 된 경우 직렬화 된 UDT (large object) 크기 제한 (현재는 2GB)으로 커질 수 있습니다. UDT의 크기에 지정 된 값을 초과할 수 없습니다는 **MaxByteSized** 필드입니다.  
  
> [!NOTE]  
>  선택적으로 구현할 수 비교를 수행 하기 위한 서버에서 사용 되지 않지만 **System.IComparable** 단일 메서드를 노출 하는 인터페이스 **CompareTo**합니다. 이 인터페이스는 UDT 값을 정확하게 비교하거나 정렬해야 하는 경우에 클라이언트 쪽에서 사용됩니다.  
  
## <a name="native-serialization"></a>네이티브 직렬화  
 만들려는 UDT의 종류에 따라 UDT에 적합한 직렬화 특성을 선택해야 합니다. **네이티브** 수 있도록 하는 매우 간단한 구조를 활용 하는 직렬화 형식 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] udt는 효율적인 네이티브 표현을 디스크에 저장할 수 있습니다. **네이티브** 는 UDT가 간단 하며 다음 유형의 필드만 포함 하는 경우 형식을 것이 좋습니다.  
  
 **bool**, **byte**, **sbyte**, **short**, **ushort**, **int**, **uint**, **long**, **ulong**, **float**, **double**, **SqlByte**, **SqlInt16**, **SqlInt32**, **SqlInt64**, **SqlDateTime**, **SqlSingle**, **SqlDouble**, **SqlMoney**, **SqlBoolean**  
  
 값 형식이 있는 필드는 위의 형식에 대 한 구성에 적합 한 후보인 **네이티브** 형식 **구조체** Visual C#, (또는 **구조** 에 알려져 됩니다 Visual Basic)입니다. 예를 들어 여 지정한 UDT는 **네이티브** 직렬화 형식으로도 지정한 다른 udt 필드가 포함 될 수 있습니다는 **네이티브** 형식입니다. 지정 해야 하는 경우 UDT 정의 더 복잡 하 고 위의 목록에 없는 데이터 형식이 포함 된는 **UserDefined** serialization 형식 대신 합니다.  
  
 **네이티브** 형식은 다음 요구 사항을 갖습니다.  
  
-   형식에 대 한 값을 지정 해서는 안 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize**합니다.  
  
-   모든 필드를 직렬화할 수 있어야 합니다.  
  
-   **된 System.Runtime.InteropServices.StructLayoutAttribute** 으로 지정 해야 **StructLayout.LayoutKindSequential** 는 UDT가 구조체가 아니라 클래스에 정의 되어 있는 경우. 이 특성은 데이터 필드의 물리적 레이아웃을 제어하며 멤버를 멤버가 실제로 나타나는 순서대로 배치하는 데 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 특성을 사용하여 값이 여러 개 포함된 UDT의 필드 순서를 결정합니다.  
  
 정의 된 UDT의 예 **네이티브** serialization에서 Point UDT를 참조 하십시오. [코딩 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)합니다.  
  
## <a name="userdefined-serialization"></a>UserDefined 직렬화  
 **UserDefined** 형식에 대 한 설정에서 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** 특성은 이진 형식에 대해 전체 개발자 제어 합니다. 지정 하는 경우는 **형식** 특성의 속성으로 **UserDefined**, 사용자 코드에서 다음을 수행 해야 합니다.  
  
-   선택적 지정 **IsByteOrdered** 특성의 속성입니다. 기본값은 **false**입니다.  
  
-   지정 된 **MaxByteSize** 속성은 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**합니다.  
  
-   구현 하는 코드를 작성 **읽기** 및 **쓰기** 구현 하 여 UDT에 대 한 메서드는 **System.Data.Sql.IBinarySerialize** 인터페이스입니다.  
  
 정의 된 UDT의 예 **UserDefined** serialization에서 Currency UDT를 참조 하십시오. [코딩 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)합니다.  
  
> [!NOTE]  
>  UDT 필드를 인덱싱하려면 UDT 필드에 네이티브 직렬화를 사용하거나 필드를 지속형 필드로 만들어야 합니다.  
  
## <a name="serialization-attributes"></a>직렬화 특성  
 특성은 직렬화를 사용하여 UDT의 저장소 표현을 생성하고 UDT를 값으로 클라이언트에 전송하는 방법을 결정합니다. 지정 해야는 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** UDT를 만들 때. **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** 클래스 udt 및 UDT에 대 한 저장소 지정 특성을 나타냅니다. 선택적으로 지정할 수는 **Serializable** 있지만 특성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 필요 하지 않습니다.  
  
 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** 속성은 다음과 같습니다.  
  
 **형식**  
 될 수 있는 직렬화 형식을 지정 **네이티브** 또는 **UserDefined**UDT의 데이터 형식에 따라 합니다.  
  
 **IsByteOrdered**  
 A **부울** 결정 하는 값 방식을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UDT에 대 한 이진 비교를 수행 합니다.  
  
 **IsFixedLength**  
 이 UDT의 모든 인스턴스 길이가 같은지 여부를 나타냅니다.  
  
 **MaxByteSize**  
 인스턴스의 최대 크기(바이트)입니다. 지정 해야 **MaxByteSize** 와 **UserDefined** serialization 형식입니다. 를 지정 하는 사용자 정의 직렬화 된 UDT에 대 한 **MaxByteSize** 사용자에 의해 정의 된 대로 serialize 된 형식에서 UDT의 총 크기를 나타냅니다. 값 **MaxByteSize** 1에서 8000 사이 여야 하거나 (전체 크기는 최대 LOB 크기를 초과할 수 없습니다) 8000 바이트 보다 큰 UDT 임을 나타내기 위해-1로 설정 해야 합니다. 10 자 문자열의 속성을 갖는 UDT는 것이 좋습니다 (**System.Char**). BinaryWriter를 사용 하 여 UDT가 serialize 하는 경우 직렬화 된 문자열의 총 크기는 유니코드 utf-16 문자는 최대 문자 수를 더한를 이진 스트림으로 직렬화 하는 작업에서 발생 한 오버 헤드의 제어 2 바이트를 곱한 당 22 바이트: 2 바이트입니다. 따라서의 값을 결정할 때 **MaxByteSize**, 직렬화 된 UDT의 전체 크기를 고려해 야 합니다: 이진 형식으로 직렬화 데이터와 serialization에서 발생 한 오버 헤드를 합한 크기입니다.  
  
 **ValidationMethodName**  
 UDT의 인스턴스가 유효한지 여부를 검사하는 데 사용되는 메서드의 이름입니다.  
  
### <a name="setting-isbyteordered"></a>IsByteOrdered 설정  
 경우는 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered** 속성이 **true**, 적용에 대 한 직렬화 된 이진 데이터를 사용할 수 있도록 보장 하는 것은 의미 체계 정보의 순서 지정 합니다. 따라서 바이트 정렬된 UDT 개체의 각 인스턴스에는 직렬화된 표현이 하나만 포함될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 직렬화된 바이트에 대한 비교 작업이 수행되면 그 결과는 동일한 비교 작업이 관리 코드에서 수행된 결과와 같아야 합니다. 다음 기능은 실행할 수 **IsByteOrdered** 로 설정 된 **true**:  
  
-   이 형식의 열에 인덱스를 만드는 기능  
  
-   이 형식의 열에 CHECK 및 UNIQUE 제약 조건과 기본 키 및 외래 키를 만드는 기능  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY, GROUP BY 및 PARTITION BY 절을 사용하는 기능. 이 경우 형식의 이진 표현이 순서를 결정하는 데 사용됩니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 비교 연산자를 사용하는 기능  
  
-   이 형식의 계산 열을 유지하는 기능  
  
 모두는 **네이티브** 및 **UserDefined** 직렬화 형식은 다음 비교 연산자를 지원 때 **IsByteOrdered** 로 설정 된 **true** :  
  
-   같음(=)  
  
-   같지 않음(!=)  
  
-   보다 큼(>)  
  
-   보다 작음(\<)  
  
-   크거나 같음(>=)  
  
-   작거나 같음(<=)  
  
### <a name="implementing-nullability"></a>Null 허용 여부 구현  
 어셈블리의 특성을 올바르게 지정하는 것 외에도 클래스는 Null 허용 여부를 지원해야 합니다. 에 로드 된 Udt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] null 인식 하지만 udt에서 null 값을 인식할 수 순서로 클래스를 구현 해야 합니다는 **INullable** 인터페이스입니다. 자세한 내용 및 UDT에서 null 허용 여부를 구현 하는 방법의 예에 대 한 참조 [코딩 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)합니다.  
  
### <a name="string-conversions"></a>문자열 변환  
 문자열 변환 하 고 udt에서를 지원 하기 위해 제공 해야 합니다는 **구문 분석** 메서드 및 **ToString** 메서드를 클래스에 있습니다. **구문 분석** 메서드를 사용 하는 문자열을 UDT로 변환할 수 있습니다. 으로 선언 되어야 합니다 **정적** (또는 **Shared** Visual basic에서), 형식의 매개 변수를 사용 하 고 **System.Data.SqlTypes.SqlString**합니다. 자세한 내용 및 구현 하는 방법의 예는 **구문 분석** 및 **ToString** 메서드 참조 [코딩 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)합니다.  
  
## <a name="xml-serialization"></a>XML 직렬화  
 Udt에서 변환을 지원 해야 합니다는 **xml** XML serialization에 대 한 계약에 따라 데이터 형식입니다. **system. Xml.serialization** 네임 스페이스 개체를 XML 형식 문서 또는 스트림으로 serialize 하는 데 사용 되는 클래스를 포함 합니다. 구현 하도록 선택할 수 **xml** 를 사용 하 여 serialization의 **IXmlSerializable** XML serialization 및 deserialization에 대 한 사용자 지정 서식을 제공 하는 인터페이스입니다.  
  
 UDT에서 명시적 변환을 수행 하는 것 외에도 **xml**, XML 직렬화를 사용 하면:  
  
-   사용 하 여 **Xquery** 로 변환 후 UDT 인스턴스 값에 대해는 **xml** 데이터 형식입니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 네이티브 XML 웹 서비스를 사용하여 매개 변수가 있는 쿼리 및 웹 메서드에서 UDT를 사용합니다.  
  
-   UDT를 사용하여 대량 로드된 XML 데이터를 받습니다.  
  
-   UDT 열이 있는 테이블이 포함된 데이터 집합을 직렬화합니다.  
  
 FOR XML 쿼리에서는 UDT가 직렬화되지 않습니다. Udt의 XML 직렬화를 표시 하는 FOR XML 쿼리를 실행 하려면 각 UDT 열을 명시적으로 변환 된 **xml** SELECT 문에서 데이터 형식입니다. 열을 명시적으로 변환할 수 있습니다 **varbinary**, **varchar**, 또는 **nvarchar**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [사용자 정의 형식 만들기](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
