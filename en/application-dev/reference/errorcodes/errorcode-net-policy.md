# Policy Management Error Codes

## 2100001 Invalid Parameter Value

**Error Message**

Invalid parameter value.

**Description**

Invalid parameter value

**Cause**

The input parameter value is not within the valid value range.

**Procedure**

Check whether the input parameter value is within the valid value range.

## 2100002 Service Connection Failure

**Error Message**

Operation failed. Cannot connect to service.

**Description**

This error code is reported if a service connection failure occurs.

**Cause**

The service is abnormal.

**Procedure**

Check whether system services are running properly.

## 2100003 System Internal Error

**Error Message**

System internal error.

**Description**

This error code is reported if a system internal error occurs.

**Cause**

1. The memory is abnormal.

2. A null pointer is present.

**Procedure**

1. Check whether the memory space is sufficient. If not, clear the memory and try again.

2. Check whether the system is normal. If not, try again later or restart the device.
