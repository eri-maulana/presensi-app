    name: "[Phase 13] Presensi Pulang — Checkout flow"
    description: "Checklist for [Phase 13] Presensi Pulang — Checkout flow - follow tasks and mark done"
    title: "[Phase 13] Presensi Pulang — Checkout flow"
    labels: ["phase-13_presensi_pulang", "todo"]
    assignees: []

    body:
      - type: markdown
        attributes:
          value: |
            ## 🎯 Purpose / Tujuan
            [Phase 13] Presensi Pulang — Checkout flow


**Instructions:** Kerjakan checklist di bawah ini satu per satu. Setiap item mewakili tugas harian yang sebaiknya dikerjakan untuk phase ini.

      - type: checkboxes
        id: tasks
        attributes:
          label: "✅ Checklist Tasks"
          options:
            - label: "Review design & requirement for [Phase 13] Presensi Pulang — Checkout flow"
            - label: "Create necessary migrations/models/controllers (backend)"
            - label: "Implement frontend components/pages as per mockup"
            - label: "Write API endpoints & validation (if applicable)"
            - label: "Manual testing & fix bugs found"
            - label: "Document the work (docs/ and update README)"

- type: textarea
  id: notes
  attributes:
    label: "📝 Notes / Catatan"
    description: "Isi catatan, blokers, atau link terkait pekerjaan di phase ini."
    placeholder: "Contoh: perlu API key, butuh akses S3, dsb."
