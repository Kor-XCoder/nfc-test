<script setup>
const scanNFC = async () => {
  try {
    const ndef = new NDEFReader();
    await ndef.scan();
    log("> Scan started");

    ndef.addEventListener("readingerror", () => {
      alert("Argh! Cannot read data from the NFC tag. Try another one?");
    });

    ndef.addEventListener("reading", ({ message, serialNumber }) => {
      alert(`> Serial Number: ${serialNumber}`);
      alert(`> Records: (${message.records.length})`);
    });
  } catch (error) {
    alert("Argh! " + error);
  }
}
</script>

<template>
  <h1>NFC Test Board</h1>
  <button @click="scanNFC" class="nfc-button">NFC 스캔</button>
</template>

<style scoped>
.nfc-button {
  background-color: #42b883;
  color: white;
  border: none;
  padding: 12px 24px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}
.nfc-button:hover {
  background-color: #369b6f;
}
</style>
