---
title: Java 확장-SQL Server 언어 확장에 대 한 SDK
description: Microsoft SQL Server 2019에 대 한 Microsoft 확장 SDK for Java의 설명
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c244d67c7f1cd1636fcd2de0b80454c96927b5d7
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65101816"
---
# <a name="microsoft-extensibility-sdk-for-java-for-sql-server"></a>Microsoft SQL Server에 대 한 Java 용 SDK 확장성

SQL Server CTP 2.5에서는 Java에 대 한 Microsoft 확장 SDK를 사용 하 여 SQL Server에 대 한 Java 프로그램을 구현할 수 있습니다. 이 SQL Server를 사용 하 여 데이터를 교환 하 고 SQL Server에서 Java 코드를 실행 하는 Java 언어 확장에 대 한 인터페이스입니다.

> [!Note]
> CTP 2.5에서 SDK는 이전 Ctp의 큰 변화입니다. 샘플 작업 했던 대신 SDK를 사용 하도록 업데이트 해야 합니다.

다운로드 합니다 [Microsoft SQL Server에 대 한 Java 용 SDK Microsoft 확장성](http://aka.ms/mssql-java-lang-extension)합니다.

## <a name="implementation-requirements"></a>구현 요구 사항

SDK 인터페이스에는 Java 런타임와 통신 하는 SQL Server에 대 한 충족 해야 하는 요구 사항 집합을 정의 합니다. 이 기본 클래스에서 일부 구현 규칙을 따르도록 할 것을 의미 합니다. 그런 다음 SQL Server Java 언어 확장을 사용 하 여 Java 클래스 및 exchange 데이터의 특정 메서드를 실행할 수 있습니다.

SDK를 사용 하는 방법의 예제를 참조 합니다 [종단 간 샘플](java-first-sample.md)합니다.

## <a name="sdk-classes"></a>SDK 클래스

이 SDK는 세 가지 클래스로 구성 됩니다.

SQL Server를 사용 하 여 데이터를 교환 하는 Java 확장 인터페이스를 정의 하는 두 가지 추상 클래스 사용 합니다.

- **AbstractSqlServerExtensionExecutor**
- **AbstractSqlServerExtensionDataset**

세 번째 클래스는 데이터 집합 개체의 구현을 포함 하는 도우미 클래스입니다. 쉽게 시작 하는 데는 선택적 클래스입니다. 이러한 클래스의 고유한 구현을 사용할 수 있습니다.

- **PrimitiveDataset**

아래 SQL Server에 대 한 세부 정보 및 Java 언어 확장의 각 클래스에 대 한 소스 코드를 따릅니다.

## <a name="abstractsqlserverextensionexecutor"></a>AbstractSqlServerExtensionExecutor

SQL Server에 대 한 Java 언어 확장에 의해 Java 코드를 실행 하는 데 사용 하는 인터페이스를 포함 하는 추상 클래스입니다.

기본 Java 클래스는이 클래스에서 상속 해야 합니다. 이 클래스에서 상속 하는 사용자 지정 클래스에서 구현 해야 할 클래스의 특정 메서드는 하는 것을 의미 합니다.

이 추상 클래스에서 상속 하는 클래스 선언에서 추상 클래스 이름으로 확장 합니다.

```java
public class <MyClass> extends AbstractSqlServerExtensionExecutor {}
```

여기에 최소한 기본 클래스를 execute(...) 메서드를 구현 해야 합니다.

### <a name="method-execute"></a>메서드 실행

Execute 메서드는 SQL Server에서 Java 코드를 호출할 Java 언어 확장을 통해 SQL Server에서 호출 되는 메서드입니다. 확인 해야이 주요 방법으로 주를 포함 하는 SQL Server에서 실행 하려는 작업입니다.

메서드 인수에 전달할 Java에서 SQL Server를 사용 하 여는 `@param` sp_execute_external_script에서 매개 변수입니다. 메서드 **실행** 이런 방식으로 해당 인수를 사용 합니다.

```java
public AbstractSqlServerExtensionDataset execute(AbstractSqlServerExtensionDataset input, LinkedHashMap<String, Object> params)  {}
```

### <a name="method-init"></a>Init 메서드

Init 메서드는 생성자 뒤 execute 메서드 전에 실행 됩니다. 이 메서드에서 execute(...) 하기 전에 수행 해야 하는 모든 작업을 수행할 수 있습니다.

```java
public void init(String sessionId, int taskId, int numtask) {}
```

### <a name="abstractsqlserverextensionexecutor-source-code"></a>AbstractSqlServerExtensionExecutor 소스 코드

소스 코드에서 아래 자세한 세부 정보를 찾을 수 있습니다.

```java
package com.microsoft.sqlserver.javalangextension;

import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionDataset;
import java.lang.UnsupportedOperationException;
import java.util.LinkedHashMap;

/**
 * Abstract class containing interface used by the Java extension
 */
public abstract class AbstractSqlServerExtensionExecutor {
    /* Supported versions of the Java extension */
    public final int SQLSERVER_JAVA_LANG_EXTENSION_V1 = 1;

    /* Members used by the extension to determine application specifics */
    protected int executorExtensionVersion;
    protected String executorInputDatasetClassName;
    protected String executorOutputDatasetClassName;

    public AbstractSqlServerExtensionExecutor() { }

    public void init(String sessionId, int taskId, int numTasks) {
        /* Default implementation of init() is no-op */
    }

    public AbstractSqlServerExtensionDataset execute(AbstractSqlServerExtensionDataset input, LinkedHashMap<String, Object> params) {
        throw new UnsupportedOperationException("AbstractSqlServerExtensionExecutor execute() is not implemented");
    }

    public void cleanup() {
        /* Default implementation of cleanup() is no-op */
    }
}
```

### <a name="abstractsqlserverextensiondataset"></a>AbstractSqlServerExtensionDataset

Java 확장에서 사용 하는 입력 및 출력 데이터를 처리 하기 위한 인터페이스를 포함 하는 추상 클래스입니다.

```java
package com.microsoft.sqlserver.javalangextension;

import java.lang.UnsupportedOperationException;

/**
 * Abstract class containing interface for handling input and output data used by the Java
 * extension.
 */
public class AbstractSqlServerExtensionDataset {
    /**
     * Column metadata interfaces
     */
    public void addColumnMetadata(int columnId, String columnName, int columnType, int precision, int scale) {
        throw new UnsupportedOperationException("addColumnMetadata is not implemented");
    }

    public int getColumnCount() {
        throw new UnsupportedOperationException("getColumnCount is not implemented");
    }

    public String getColumnName(int columnId) {
        throw new UnsupportedOperationException("getColumnName is not implemented");
    }

    public int getColumnPrecision(int columnId) {
        throw new UnsupportedOperationException("getColumnPrecision is not implemented");
    }

    public int getColumnScale(int columnId) {
        throw new UnsupportedOperationException("getColumnScale is not implemented");
    }

    public int getColumnType(int columnId) {
        throw new UnsupportedOperationException("getColumnNullMap is not implemented");
    }

    public boolean[] getColumnNullMap(int columnId) {
        throw new UnsupportedOperationException("getColumnNullMap is not implemented");
    }

    /**
     * Adding column interfaces
     */
    public void addIntColumn(int columnId, int[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addIntColumn is not implemented");
    }

    public void addBooleanColumn(int columnId, boolean[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addBooleanColumn is not implemented");
    }

    public void addLongColumn(int columnId, long[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addLongColumn is not implemented");
    }

    public void addFloatColumn(int columnId, float[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addFloatColumn is not implemented");
    }

    public void addDoubleColumn(int columnId, double[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addDoubleColumn is not implemented");
    }

    public void addShortColumn(int columnId, short[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addShortColumn is not implemented");
    }

    public void addStringColumn(int columnId, String[] rows) {
        throw new UnsupportedOperationException("addStringColumn is not implemented");
    }

    public void addBinaryColumn(int columnId, byte[][] rows) {
        throw new UnsupportedOperationException("addBinaryColumn is not implemented");
    }

    /**
     * Retrieving column interfaces
     */
    public int[] getIntColumn(int columnId) {
        throw new UnsupportedOperationException("getIntColumn is not implemented");
    }

    public long[] getLongColumn(int columnId) {
        throw new UnsupportedOperationException("getLongColumn is not implemented");
    }

    public float[] getFloatColumn(int columnId) {
        throw new UnsupportedOperationException("getFloatColumn is not implemented");
    }

    public short[] getShortColumn(int columnId) {
        throw new UnsupportedOperationException("getShortColumn is not implemented");
    }

    public boolean[] getBooleanColumn(int columnId) {
        throw new UnsupportedOperationException("getBooleanColumn is not implemented");
    }

    public double[] getDoubleColumn(int columnId) {
        throw new UnsupportedOperationException("getDoubleColumn is not implemented");
    }

    public String[] getStringColumn(int columnId) {
        throw new UnsupportedOperationException("getStringColumn is not implemented");
    }

    public byte[][] getBinaryColumn(int columnId) {
        throw new UnsupportedOperationException("getBinaryColumn is not implemented");
    }
}
```

### <a name="primitivedataset"></a>PrimitiveDataset

이 클래스의 구현인 **AbstractSqlServerExtensionDataset** 단순 형식 기본 형식 배열로 저장 합니다. 사용 하거나 사용 된 도우미 클래스로 서 단순히 SDK에서 제공 됩니다.

상속 되는 고유한 클래스를 구현 해야 하는이 클래스를 사용 하지 않는 경우 **AbstractSqlServerExtensionDataset**합니다.  

```java
package com.microsoft.sqlserver.javalangextension;

import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionDataset;
import java.lang.IllegalArgumentException;
import java.util.HashMap;
import java.util.Map;
import java.util.Map.Entry;

/**
 * Implementation of AbstractSqlServerExtensionDataset that stores
 * simple types as primitives arrays
 */
public class PrimitiveDataset extends AbstractSqlServerExtensionDataset {
    Map<Integer, String>  columnNames;
    Map<Integer, Integer> columnTypes;
    Map<Integer, Integer> columnPrecisions;
    Map<Integer, Integer> columnScales;
    Map<Integer, Object>  columns;
    Map<Integer, boolean[]> columnNullMaps;

    public PrimitiveDataset() {
        columnTypes = new HashMap<>();
        columnNames = new HashMap<>();
        columnPrecisions = new HashMap<>();
        columnScales = new HashMap<>();
        columns = new HashMap<>();
        columnNullMaps = new HashMap<>();
    }

    /**
     * Column metadata interfaces. Metadata is stored in a hash map, using the column ID as the key
     */
    public void addColumnMetadata(int columnId, String columnName, int sqlType, int precision, int scale) {
        if (columnTypes.containsKey(columnId))
        {
            throw new IllegalArgumentException("Metadata for column ID #: " + columnId + " already exists");
        }

        columnTypes.put(columnId, sqlType);
        columnNames.put(columnId, columnName);
        columnPrecisions.put(columnId, precision);
        columnScales.put(columnId, scale);
    }

    public int getColumnCount() {
        return columnTypes.size();
    }

    public String getColumnName(int columnId) {
        checkColumnMetadata(columnId);
        return columnNames.get(columnId);
    }

    public int getColumnPrecision(int columnId) {
        checkColumnMetadata(columnId);
        return columnPrecisions.get(columnId).intValue();
    }

    public int getColumnScale(int columnId) {
        checkColumnMetadata(columnId);
        return columnScales.get(columnId).intValue();
    }

    public int getColumnType(int columnId) {
        checkColumnMetadata(columnId);
        return columnTypes.get(columnId).intValue();
    }

    public boolean[] getColumnNullMap(int columnId) {
        checkColumnMetadata(columnId);
        return columnNullMaps.get(columnId);
    }

    /**
     * Adding column data interfaces. Column data is stored in a hash map, using the column ID as the key and
     * an array of the corresponding type representing each row. Primitives cannot be null, thus null values
     * are represented by an additional boolean array containing a flag to indicate if that value is null.
     * A null indicator array indicates that there are no null values in that column.
     */
    public void addIntColumn(int columnId, int[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addBooleanColumn(int columnId, boolean[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    };

    public void addLongColumn(int columnId, long[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addFloatColumn(int columnId, float[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addDoubleColumn(int columnId, double[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addShortColumn(int columnId, short[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addStringColumn(int columnId, String[] rows) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
    }

    public void addBinaryColumn(int columnId, byte[][] rows) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
    }

    /**
     * Retreiving column data interfaces. For primitive types, calling getColumnNullMap() for the column ID
     * will return the boolean array indicating null values.
     */
    public int[] getIntColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (int[])columns.get(columnId);
    }

    public long[] getLongColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (long[])columns.get(columnId);
    }

    public float[] getFloatColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (float[])columns.get(columnId);
    }

    public short[] getShortColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (short[])columns.get(columnId);
    }

    public boolean[] getBooleanColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (boolean[])columns.get(columnId);
    }

    public double[] getDoubleColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (double[])columns.get(columnId);
    }

    public String[] getStringColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (String[])columns.get(columnId);
    }

    public byte[][] getBinaryColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (byte[][])columns.get(columnId);
    }

    private void checkColumnMetadata(int columnId)
    {
        if (!columnTypes.containsKey(columnId)) {
            throw new IllegalArgumentException("Metadata for column ID #: " + columnId + " does not exist");
        }
    }
}
```

## <a name="next-steps"></a>다음 단계

+ [Java 샘플 SDK를 사용 하 여 종단 간](java-first-sample.md)
+ [SQL Server에서 Java를 호출 하는 방법](howto-call-java-from-sql.md)
+ [SQL Server에서 Java 확장](extension-java.md)
+ [Java와 SQL Server 데이터 형식](java-sql-datatypes.md)
