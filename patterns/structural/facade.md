### Facade

The facade pattern (also spelled as "fachada") is a commonly used software design pattern in object-oriented programming. Analogous to a facade in architecture, a facade is an object that serves as a front-end interface that masks more complex underlying or structural code. It provides a simplified interface for accessing a set of related subsystems or classes, making interaction with the system easier without needing to know the internal details.

**Example:**

In this example, we will simulate the operation of a computer using the facade pattern. The computer consists of various components such as CPU, memory, and hard drive. The ComputerFacade will simplify the interaction with these components.

1. We define classes for computer components: CPU, Memory, and HardDrive. These classes have methods to perform various operations, such as freezing the CPU, loading data into memory, and reading from the hard drive.

```
class CPU {
  freeze() { console.log("CPU Frozen...") }
  jump(position) { console.log("Jump to position " + position) }
  execute() { console.log("Execute CPU...") }
}

class Memory {
  load(position, data) { console.log("Load data at position " + position + ": " + data) }
}

class HardDrive {
  read(lba, size) { console.log("Read from LBA " + lba + " with size " + size) }
}
```

2. We create the ComputerFacade, which provides a simplified interface for interacting with computer components. In the start() method, components are used coherently and mask complex details.

```
class ComputerFacade {
  constructor() {
    this.processor = new CPU();
    this.ram = new Memory();
    this.hdd = new HardDrive();
  }

  start() {
    this.processor.freeze();
    this.ram.load(this.BOOT_ADDRESS, this.hdd.read(this.BOOT_SECTOR, this.SECTOR_SIZE));
    this.processor.jump(this.BOOT_ADDRESS);
    this.processor.execute();
  }
}

```

3.Finally, we create an instance of ComputerFacade and use its start() method to simulate the computer's booting process.

```
let computer = new ComputerFacade();
computer.start();

```

**Final Code:**

```
// Definition of the CPU class representing the central processing unit.
class CPU {
  freeze() { console.log("CPU Frozen...") } // Method to freeze the CPU.
  jump(position) { console.log("Jump to position " + position) } // Method to jump to a specific position.
  execute() { console.log("Execute CPU...") } // Method to execute the CPU.
}

// Definition of the Memory class representing the computer's memory.
class Memory {
  load(position, data) { console.log("Load data at position " + position + ": " + data) } // Method to load data into memory.
}

// Definition of the HardDrive class representing the computer's hard drive.
class HardDrive {
  read(lba, size) { console.log("Read from LBA " + lba + " with size " + size) } // Method to read from the hard drive.
}

// Definition of the ComputerFacade class that acts as a facade to interact with computer components.
class ComputerFacade {
  constructor() {
    this.processor = new CPU(); // Create an instance of CPU.
    this.ram = new Memory(); // Create an instance of Memory.
    this.hdd = new HardDrive(); // Create an instance of Hard Drive.
  }

  start() {
    this.processor.freeze(); // Freeze the CPU.
    this.ram.load(this.BOOT_ADDRESS, this.hdd.read(this.BOOT_SECTOR, this.SECTOR_SIZE)); // Load data into memory from the hard drive.
    this.processor.jump(this.BOOT_ADDRESS); // Jump to the start address.
    this.processor.execute(); // Execute the CPU.
  }
}

// Create an instance of ComputerFacade and use it to simulate the computer's boot process.
let computer = new ComputerFacade();
computer.start();

// Expected output:
// CPU Frozen...
// Load data at position BOOT_ADDRESS: Read from LBA BOOT_SECTOR with size SECTOR_SIZE
// Jump to position BOOT_ADDRESS
// Execute CPU...

```
