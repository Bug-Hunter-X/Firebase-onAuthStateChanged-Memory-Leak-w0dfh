# Firebase onAuthStateChanged Memory Leak

This repository demonstrates a common issue with Firebase's `onAuthStateChanged` listener: memory leaks.  If the listener is not unsubscribed when it's no longer needed, it continues to consume resources, potentially leading to performance degradation.

## Problem

The `onAuthStateChanged` function returns an unsubscribe function.  Failing to call this unsubscribe function will cause a persistent listener that keeps consuming resources, even after the component that uses the listener is unmounted or the application closes. 

## Solution

The solution is to store the unsubscribe function returned by `onAuthStateChanged` and call it when the listener is no longer required.  This is typically done in a cleanup function (like `componentWillUnmount` in a React component or when the component is destroyed).