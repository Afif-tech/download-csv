<template>
  <div>
    <h1>Asset Management</h1>
    <table border="1">
      <thead>
        <tr>
          <th>Asset Name</th>
          <th>Department</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="asset in assets" :key="asset.assetName">
          <td>{{ asset.assetName }}</td>
          <td>{{ asset.department }}</td>
        </tr>
      </tbody>
    </table>
    <button @click="downloadCSV">Download CSV</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      assets: [
        { assetName: "Printer", department: "HR" },
        { assetName: "Monitor", department: "IT" },
        { assetName: "Barcode Scanner", department: "ACCOUNT" },
      ],
    };
  },
  methods: {
    downloadCSV() {
      const headers = "Asset Name,Department\n";
      const rows = this.assets
        .map((asset) => `${asset.assetName},${asset.department}`)
        .join("\n");

      const csvContent = headers + rows;
      const blob = new Blob([csvContent], { type: "text/csv;charset=utf-8;" });
      const link = document.createElement("a");

      link.href = URL.createObjectURL(blob);
      link.download = "assets.csv";
      link.click();
    },
  },
};
</script>

<style>
h1 {
  font-family: Arial, sans-serif;
  color: #333;
  text-align: center;
}

table {
  width: 50%;
  margin: 20px auto;
  border-collapse: collapse;
}
th, td {
  padding: 10px;
  text-align: left;
}
button {
  margin: 20px auto;
  display: block;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}
</style>