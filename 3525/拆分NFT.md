你可以通过下面的步骤将tokenID=100的token进行拆分，拆分到另一个tokenId并且他们使用同一个slot：

1. **创建新的Token ID：**
   调用`_createDerivedTokenId`函数，为你的新token生成一个新的token ID。例如：
   ```solidity
   uint256 newTokenId = _createDerivedTokenId(100);
   ```

2. **铸造新的Token：**
   使用新生成的token ID调用`_mint`函数，将新的token铸造到你的地址，并确保slot与原token相同。例如：
   ```solidity
   _mint(msg.sender, newTokenId, slotOf(100), 0);
   ```

3. **转移部分余额：**
   使用`_transferValue`函数，将原token ID的部分余额转移到新的token ID。例如，将20个余额从tokenID=100转移到新的token ID：
   ```solidity
   _transferValue(100, newTokenId, 20);
   ```

完整代码示例：
```solidity
// 生成新的token ID
uint256 newTokenId = _createDerivedTokenId(100);

// 铸造新的token，slot与原token相同
_mint(msg.sender, newTokenId, slotOf(100), 0);

// 从tokenID=100转移20个余额到新的token ID
_transferValue(100, newTokenId, 20);
```

通过上述步骤，你将成功地将tokenID=100的token拆分一部分到新的token ID，并且它们使用相同的slot。希望这能帮助到你！如果有其他问题，欢迎继续提问。