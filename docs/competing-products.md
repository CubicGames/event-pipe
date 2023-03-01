# State Of The Art

## eventeum

```mermaid

classDiagram

    class WebSocketService {
        WebSocketClient socketClient
        onWebSocketClose(): void
    }

    class ChainBootstraper {
        Logger log
        SubscriptionService subscriptionService
        EventFilterConfiguration filterConfiguration
        onApplicationEvent(ContextRefreshedEvent event): void
        registerFilter(ContractEventFilter filter, boolean broadcast): void
    }

    class WebSocketReconnectionManager {
        reconnect(WebSocketClient client): void
    }

    class Web3jUtil {
        Map<ParameterType, TypeMapping> typeMappings
        addUintMappings(int interval, int max): void
        addUintArrayMappings(int interval, int max): void
        addIntMappings(int interval, int max): void
        addIntArrayMappings(int interval, int max): void
        addBytesMappings(int interval, int max): void
        addBytesArrayMappings(int interval, int max): void
    }

    class BloomFilterUtil {
        getBloomBits(ContractEventFilter filter): BloomFilterBits
        bloomFilterMatch(String bloomFilterHex, BloomFilterBits bitsToMatch): boolean
    }

    class Web3jService {
        Web3j web3j
        ContractEventDetailsFactory eventDetailsFactory
        AsyncTaskService asyncTaskService
        retrieveEvents(ContractEventFilter eventFilter,BigInteger startBlock, BigInteger endBlock): List<ContractEventDetails>
        registerEventListener(ContractEventFilter eventFilter,ContractEventListener eventListener): FilterSubscription
        getCurrentBlockNumber(): BigInteger
        getBlock(String blockHash, boolean fullTransactionObjects): Optional<Block>
        getEventsForFilter(ContractEventFilter filter, BigInteger blockNumber): List<ContractEventDetails>
    }

    class BlockchainServiceFactory {
        << interface >>
        create(Node node): BlockchainService
    }

    class Web3jEventParameterConverter {
        Map<String, EventParameterConverter<Type>> typeConverters
        convert(Type toConvert): EventParameter
    }

    class AsyncTaskService {
        execute(String executorName, Runnable task): void
        submit(String executorName, Callable<T> task): Future<T>
    }  
  
    
  
```
