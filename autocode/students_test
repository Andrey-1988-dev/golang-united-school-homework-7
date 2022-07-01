package coverage

import (
	"os"
	"reflect"
	"testing"
	"time"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW
func TestPeople_Len(t *testing.T) {
	tests := []struct {
		name           string
		p              People
		numberOfPeople int
		want           int
	}{
		{
			name:           "10 people",
			numberOfPeople: 10,
			want:           10,
		},
		{
			name:           "0 people",
			numberOfPeople: 0,
			want:           0,
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			for i := 0; i < tt.numberOfPeople; i++ {
				tt.p = append(tt.p, Person{})
			}
			if got := tt.p.Len(); got != tt.want {
				t.Errorf("Len() = %v, want %v", got, tt.want)
			}
		})
	}
}

func TestPeople_Less(t *testing.T) {
	peoples := People{
		{
			firstName: "Albert",
			lastName:  "Einstein",
			birthDay:  time.Date(1879, time.March, 14, 0, 0, 0, 0, time.UTC),
		},
		{
			firstName: "Albert",
			lastName:  "Abramovitz",
			birthDay:  time.Date(1879, time.March, 14, 0, 0, 0, 0, time.UTC),
		},
		{
			firstName: "Rudolf",
			lastName:  "Einstein",
			birthDay:  time.Date(1879, time.March, 14, 0, 0, 0, 0, time.UTC),
		},
		{
			firstName: "Hermann",
			lastName:  "Einstein",
			birthDay:  time.Date(1847, time.August, 30, 0, 0, 0, 0, time.UTC),
		},
	}

	type args struct {
		i int
		j int
	}
	tests := []struct {
		name string
		p    People
		args args
		want bool
	}{
		{
			name: "p[i].lastName >= p[j].lastName",
			p:    peoples,
			args: args{
				i: 0,
				j: 0,
			},
			want: false,
		},
		{
			name: "p[i].lastName < p[j].lastName",
			p:    peoples,
			args: args{
				i: 1,
				j: 0,
			},
			want: true,
		},
		{
			name: "p[i].firstName >= p[j].firstName",
			p:    peoples,
			args: args{
				i: 2,
				j: 0,
			},
			want: false,
		},
		{
			name: "p[i].firstName < p[j].firstName",
			p:    peoples,
			args: args{
				i: 0,
				j: 2,
			},
			want: true,
		},
		{
			name: "p[i].birthDay <= p[j].birthDay",
			p:    peoples,
			args: args{
				i: 3,
				j: 0,
			},
			want: false,
		},
		{
			name: "p[i].birthDay > p[j].birthDay",
			p:    peoples,
			args: args{
				i: 0,
				j: 3,
			},
			want: true,
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			if got := tt.p.Less(tt.args.i, tt.args.j); got != tt.want {
				t.Errorf("Less() = %v, want %v", got, tt.want)
			}
		})
	}
}

func TestPeople_Swap(t *testing.T) {
	peoples := People{
		{
			firstName: "Albert",
			lastName:  "Einstein",
			birthDay:  time.Date(1879, time.March, 14, 0, 0, 0, 0, time.UTC),
		},
		{
			firstName: "Hermann",
			lastName:  "Einstein",
			birthDay:  time.Date(1847, time.August, 30, 0, 0, 0, 0, time.UTC),
		},
	}
	type args struct {
		i int
		j int
	}
	tests := []struct {
		name string
		p    People
		args args
	}{
		{
			name: "Change the same people",
			p:    peoples,
			args: args{
				i: 0,
				j: 0,
			},
		},
		{
			name: "Change different people",
			p:    peoples,
			args: args{
				i: 0,
				j: 1,
			},
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			oldI := tt.p[tt.args.i]
			oldJ := tt.p[tt.args.j]
			tt.p.Swap(tt.args.i, tt.args.j)
			if oldI != tt.p[tt.args.j] {
				t.Errorf("old i (%v) != new j (%v)", oldI, tt.p[tt.args.j])
			} else if oldJ != tt.p[tt.args.i] {
				t.Errorf("old j (%v) != new i (%v)", oldJ, tt.p[tt.args.i])
			}
		})
	}
}

func TestNew(t *testing.T) {
	type args struct {
		str string
	}
	var tests = []struct {
		name    string
		args    args
		want    *Matrix
		wantErr bool
	}{
		{
			name: "Different columns",
			args: args{
				str: "1 1 1\n2 2\n3",
			},
			want:    nil,
			wantErr: true,
		},
		{
			name: "Correct matrix",
			args: args{
				str: "1 1 1\n2 2 2\n3 3 3",
			},
			want: &Matrix{
				rows: 3,
				cols: 3,
				data: []int{1, 1, 1, 2, 2, 2, 3, 3, 3},
			},
			wantErr: false,
		},
		{
			name: "Not a numeric value",
			args: args{
				str: "1 1 1\n2 V 2\n3 3 3",
			},
			want:    nil,
			wantErr: true,
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			got, err := New(tt.args.str)
			if (err != nil) != tt.wantErr {
				t.Errorf("New() error = %v, wantErr %v", err, tt.wantErr)
				return
			}
			if !reflect.DeepEqual(got, tt.want) {
				t.Errorf("New() got = %v, want %v", got, tt.want)
			}
		})
	}
}

func TestMatrix_Rows(t *testing.T) {
	type fields struct {
		rows int
		cols int
		data []int
	}
	tests := []struct {
		name   string
		fields fields
		want   [][]int
	}{
		{
			name: "Correct matrix",
			fields: fields{
				rows: 3,
				cols: 3,
				data: []int{1, 1, 1, 2, 2, 2, 3, 3, 3},
			},
			want: [][]int{
				{1, 1, 1},
				{2, 2, 2},
				{3, 3, 3},
			},
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			m := Matrix{
				rows: tt.fields.rows,
				cols: tt.fields.cols,
				data: tt.fields.data,
			}
			if got := m.Rows(); !reflect.DeepEqual(got, tt.want) {
				t.Errorf("Rows() = %v, want %v", got, tt.want)
			}
		})
	}
}

func TestMatrix_Cols(t *testing.T) {
	type fields struct {
		rows int
		cols int
		data []int
	}
	tests := []struct {
		name   string
		fields fields
		want   [][]int
	}{
		{
			name: "Correct matrix",
			fields: fields{
				rows: 3,
				cols: 3,
				data: []int{1, 1, 1, 2, 2, 2, 3, 3, 3},
			},
			want: [][]int{
				{1, 2, 3},
				{1, 2, 3},
				{1, 2, 3},
			},
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			m := Matrix{
				rows: tt.fields.rows,
				cols: tt.fields.cols,
				data: tt.fields.data,
			}
			if got := m.Cols(); !reflect.DeepEqual(got, tt.want) {
				t.Errorf("Cols() = %v, want %v", got, tt.want)
			}
		})
	}
}

func TestMatrix_Set(t *testing.T) {
	type fields struct {
		rows int
		cols int
		data []int
	}
	type args struct {
		row   int
		col   int
		value int
	}
	tests := []struct {
		name   string
		fields fields
		args   args
		want   bool
	}{
		{
			name:   "row < 0",
			fields: fields{},
			args: args{
				row:   -1,
				col:   1,
				value: 1,
			},
			want: false,
		},
		{
			name: "m.rows <= row",
			fields: fields{
				rows: 1,
				cols: 1,
				data: []int{},
			},
			args: args{
				row:   2,
				col:   1,
				value: 1,
			},
			want: false,
		},
		{
			name:   "col < 0",
			fields: fields{},
			args: args{
				row:   1,
				col:   -1,
				value: 1,
			},
			want: false,
		},
		{
			name: "m.cols <= col",
			fields: fields{
				rows: 1,
				cols: 1,
				data: []int{},
			},
			args: args{
				row:   1,
				col:   2,
				value: 1,
			},
			want: false,
		},
		{
			name: "Correct matrix",
			fields: fields{
				rows: 1,
				cols: 3,
				data: []int{1, 2, 3},
			},
			args: args{
				row:   0,
				col:   0,
				value: 1,
			},
			want: true,
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			m := &Matrix{
				rows: tt.fields.rows,
				cols: tt.fields.cols,
				data: tt.fields.data,
			}
			if got := m.Set(tt.args.row, tt.args.col, tt.args.value); got != tt.want {
				t.Errorf("Set() = %v, want %v", got, tt.want)
			}
		})
	}
}
